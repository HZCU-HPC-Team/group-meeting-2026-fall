# perf：给程序做"体检"

> 本周重点。这里分四块：**它是什么** → **三件套各干什么** → **我怎么采集（命令/参数/环境/次数）** → **数据怎么读、说明了什么**。
> 采集在 `hzcu-hpct`（Ubuntu 22.04，128 核，Slurm）上做；命令与脚本已备好：`scripts/perf-stat.sh`、`scripts/perf-record.sh`。

---

## 1. perf 是什么

`perf` 是 Linux 内核自带的性能分析工具，背后是内核的 **perf_events** 子系统，它同时吃两种数据源：

| 数据源 | 原理 | 能回答的问题 |
|---|---|---|
| **硬件计数器（PMU）** | CPU 里的 Performance Monitoring Unit 有固定几个可编程计数器，能精确数 cycles、instructions、cache miss、branch miss | "这段代码到底算得多还是等内存多？" |
| **采样（sampling）** | 让某个事件（如 cycles）溢出时触发中断，内核记下当时的 **IP（指令地址）+ 调用栈** | "时间花在哪个函数/哪一行？" |

硬件计数器是**精确计数**（跑一次 = 一个总数），采样是**统计推断**（按比例外推），两者互补：`stat` 给"体质报告"，`record/report` 给"热点地图"。

> 注意：`perf` 的用户态工具和内核版本强绑定，装的包叫 `linux-tools-$(uname -r)`。`hzcu-hpct` 是 Ubuntu 22.04，先 `perf --version` 确认有，没有就 `sudo apt install linux-tools-$(uname -r) linux-tools-common`。

---

## 2. 三件套各干什么（别混）

| 命令 | 一句话 | 输出 | 什么时候用 |
|---|---|---|---|
| `perf stat` | **计数**：整段程序跑了多少 cycles/instructions/miss | 一行行数字 + 比率 | 判断"计算密集还是访存密集"、算 IPC |
| `perf record` | **采样**：按频率抓 IP 和调用栈，写进 `perf.data` | 一个数据文件（默认 `perf.data`） | 想知道"哪段代码最热" |
| `perf report` | **读** `perf.data` | 交互式树 / `--stdio` 文本 | 看热点函数占比、调用链 |

三个命令的关系：`record` 只负责"存"，`report` 只负责"读"，`stat` 是另一条独立路线（不落文件）。

常用参数：

```bash
perf stat   -e <事件列表> -r <重复次数> -- <命令>     # -e 选事件，-r 3 = 跑 3 遍取平均/看波动
perf record -F 999 -g -o perf.data -- <命令>          # -F 采样频率(Hz)，-g 记调用栈
perf report --stdio --sort symbol -i perf.data        # 文本模式，按函数聚合
perf annotate --stdio -s SumDistance                  # 下钻到汇编/源码行级
```

---

## 3. 采集方案（命令 / 参数 / 环境 / 次数）

### 3.1 环境

| 项 | 值 |
|---|---|
| 机器 | `hzcu-hpct`（`ssh -p 9446 cyp@10.61.190.8`），128 逻辑核 |
| OS | Ubuntu 22.04（OpenSSH 8.9p1 / 内核版本 `uname -r` 现场确认） |
| 编译器 | 系统 `gcc`（`gcc --version` 现场记录） |
| 负载 | 赛题 `pivot`，输入 `uniformvector-2dim-5h.txt`（dim=2, n=500, k=2） |
| 干扰控制 | `taskset -c 0` 绑核；不同时跑别的重活；每项重复 3 次看波动 |

### 3.2 编译（perf 前必须带 `-g`，否则 `report` 只有地址没有函数名）

```bash
gcc -O2 -g -fno-omit-frame-pointer -o pivot_prof pivot.c -lm
```

### 3.3 `perf stat`：一次跑完，4 类关键事件

```bash
# 1) 先确认权限（perf_event_paranoid 必须是 <=1，否则普通用户读不到计数器）
cat /proc/sys/kernel/perf_event_paranoid

# 2) 计数，重复 3 次（-r 3 会连续跑 3 遍，给出均值与标准差）
perf stat -r 3 \
  -e task-clock,cycles,instructions,cache-references,cache-misses,branch-instructions,branch-misses,context-switches,page-faults \
  taskset -c 0 ./pivot_prof uniformvector-2dim-5h.txt > run_prof.log
```

说明：
- `-r 3`：赛题官方取 5 次均值，我这里 3 次够看波动（单次 ~40 s 级，3 次 ~2 min，可接受）；
- `taskset -c 0`：绑到 0 号核，减少迁移带来的噪声（本程序单线程）；
- 输出重定向到 `run_prof.log`：perf 的统计走 stderr，程序的迭代日志走 stdout，两边都留档才不会互相盖掉。

### 3.4 `perf record` + `perf report`：找热点

```bash
# 采样：999 Hz ≈ 每秒 1000 个样本；-g 记调用栈，-o 指定文件名
perf record -F 999 -g -o perf.data -- taskset -c 0 ./pivot_prof uniformvector-2dim-5h.txt > run_rec.log

# 看报告（文本版，适合贴进文档）
perf report -i perf.data --stdio --sort symbol --percent-limit 0.5

# 再往下钻到函数内部（哪一行/哪条指令最热）
perf annotate -i perf.data --stdio -s SumDistance
```

- `-F 999` 而不是默认：4096 Hz 会让采样开销明显（本程序一次只跑 40 s，999 Hz 已能拿 ~4 万个样本，足够稳）；
- `-g` 记调用栈：能看出 `SumDistance` 是被 `Combination` 调进来的（占比 99% 时这个信息不重要，但采样少的时候很有用）；
- 次数：`record` 跑 1 次即可（采样是统计量，样本量大就稳）；报告结论若和 `stat` 冲突，再补一次。

### 3.5 记录模板

采集完把数据填这里（`data/perf-template.md` 有同样的表）：

| 项目 | 值 |
|---|---|
| 命令 | `perf stat -r 3 -e task-clock,cycles,instructions,cache-references,cache-misses,branch-instructions,branch-misses ...` |
| 参数含义 | `-r 3` 重复 3 次；`-e` 指定计数器；`taskset -c 0` 绑核 |
| 环境 | hzcu-hpct / Ubuntu 22.04 / gcc ??.? / `uname -r` = ?? |
| 次数 | stat 3 次 × 1 轮；record 1 次（999 Hz） |
| 结果 | 见下表 |
| 备注 | `perf_event_paranoid` = ?；是否有 turbo/频率波动 |

---

## 4. 数据怎么读：判定"计算密集 vs 访存密集"

### 4.1 先看三个比率

| 指标 | 算法 | 含义 |
|---|---|---|
| **IPC** | `instructions / cycles` | 每个周期退休多少条指令。现代 x86 宽发射，理论 4~6；实测 **>1.5 偏计算**，**<0.8 说明大量时间在等（内存/分支/依赖）** |
| **cache miss 率** | `cache-misses / cache-references` | 末级缓存（LLC）缺失比例。**>10% 往往意味着喂不饱 CPU** |
| **branch miss 率** | `branch-misses / branch-instructions` | 分支预测失败率。**>5% 说明控制流不友好**（循环边界、条件跳转不可预测） |

### 4.2 再结合程序结构验证判断

`pivot` 的内层循环是：

```c
for (i...) for (j...) {                 // n × n = 250000 个点对
    chebyshev = max over ki(|r[i][ki] - r[j][ki]|);   // k=2
    chebyshevSum += chebyshev;
}
```

- 工作集：`rebuiltCoord` 只有 `n*k*8 = 8 KB` → **整个数组常驻 L1（32~48 KB）**；
- 每个内层迭代是 `2 次 double 减法 + 2 次 fabs + 2 次比较 + 1 次加法`，几乎没有新内存；
- 因此**合理预期**：`cache-misses` 极低、IPC 偏高（1.5~3）、branch-misses 低 → **计算密集型（更准确说是"ALU/FP 与串行依赖受限"，不是访存受限）**。

> 这条"预期"就是判断标准：**如果实测 cache-misses 很高，说明我的模型理解错了，要回去查**（比如 `rebuiltCoord` 没命中、或 malloc 造成 TLB/page fault 开销）。**数据是用来证伪的，不是用来凑结论的。**

### 4.3 时间分布上还要看一处反直觉的点

`SumDistance()` 每次被调用都会 `malloc(sizeof(double)*n*k)` 并在结尾 `free`：

- 单次 ~8 KB，`malloc` 大概率走 fastbin，很便宜；
- 但它被调用 `C(500,2) = 124750` 次 → 12 万次 malloc/free 累计开销 + **page-faults** 计数会体现出来；
- `perf stat` 里 `page-faults` 和 `context-switches` 就是留给这类开销的指标。

---

## 5. 预期会看到的热点（以及为什么大概率是 `SumDistance`）

| 函数 | 复杂度 | 每次组合的迭代量 | 全程序累计 |
|---|---|---|---|
| `Combination` | 递归枚举 `C(n,k)` 组 | 组合数 124750 | 调用 `SumDistance` 124750 次 |
| `SumDistance` · 重建坐标 | `n·k·dim` | 500×2×2 = 2000 次 | ~2.5×10⁸ 次浮点运算 |
| `SumDistance` · 切比雪夫求和 | `n²·k` | 500×500×2 = 500000 次比较 | **~6.24×10¹⁰ 次** |
| main · 排序/IO | `C(n,k)·M` 级但只搬指针 | — | 可忽略 |

**结论**：`SumDistance` 的第二个双重循环占了 ~99% 的指令量，`perf report` 里应该看到它独占鳌头，`Combination` 只占调用与少量递归开销（不含内联进它的部分）。这与讲师课上的预判一致——但**结论要以实测数据为准**，我的预期只用来校验"采样是否可信"。

---

## 6. 选做：把热点交给 AI 之后，我自己理解的"为什么慢 / 怎么改"

**为什么慢**（除算法复杂度外的二级原因）：

1. **重复计算**：`rebuiltCoord` 里每个元素是 `d(point_i, pivot_k)`——**它跟"这一组其它 pivot 选的是谁"无关**。但代码每次换组合都从头重算，等于把同一个距离算了 `C(n,k)×k` 次；
2. **`pow(x,2)` 用错了**：`pow` 是通用幂函数，即使被优化成 `x*x`，`-O0` 下也是真的函数调用（本机实测 `-O0` 296 s vs `-O2` 41 s，7 倍差距里有一部分就是它）；
3. **`n²` 全量枚举**：`(i,j)` 和 `(j,i)` 对称、`i==j` 项为 0，实际只需算 `n(n-1)/2 ≈ 12.5 万` 对，代码算了 25 万对——**白算一倍**；
4. **每次组合 `malloc/free`**：可以提到循环外一次分配；
5. **单线程**：`C(500,2)` 组之间完全独立，本该并行。

**可以怎么改（W04 动手，本周只判断不实现）**：

| 改法 | 预期收益 | 风险/代价 |
|---|---|---|
| 预计算 `n×n` 距离矩阵（250k doubles = 2 MB），重建坐标变成查表 | 消掉全部 `pow/sqrt`（~2.5×10⁸ 次） | 内存 +2 MB，可接受 |
| 只算 `i<j` 再 ×2 | 内层减半 | 无，纯收益 |
| 把 `ki` 提到最内层、按行连续访问 | 更好的向量化/更少的地址计算 | 需重排数据布局 |
| 组合间 OpenMP 并行（128 核） | 接近线性 | 结果需确定性合并（先存局部 top/bottom 再归并） |
| 对 k=2 用"按第一维排序 + 扫描"把 `O(n²)` 降到 `O(n log n)` | 数量级 | 推导容易出错，必须有 refer 兜底 |
| 去掉 `Combination` 里的迭代 `printf` | 去掉纯写 IO 开销 | 手册允许删（注释里写了） |

> 纪律：每改一步都 `diff result.txt refer-2dim-5h.txt`。加速比只有在结果仍逐字节一致时才作数。

---

## 7. 本机（Windows）没有 perf 时我做了什么（这是一次"妥协"，也记录下失败的那条路）

本机是 Windows，没有 Linux perf（也确认过本机没装 WSL，无法绕过去）。为了不让"热点"完全悬空，我试了两条路：

**路线 A：gprof（失败，但值得记下来）**

```powershell
gcc -O2 -pg -fno-inline -o pivot_pg2.exe pivot.c -lm
.\pivot_pg2.exe .\uniformvector-2dim-5h.txt
gprof .\pivot_pg2.exe gmon.out
```

结果：`gmon.out` 生成了，但 flat profile 是空的（`no time propagated`）。原因有两层：mingw 的 `-pg` 只可靠地埋了 `mcount` 计数，**采样是靠 `profil()`，在 64 位 Windows 上不生效**；再加上 `-O2` 会把 `SumDistance` 内联掉，连函数都没了。→ **教训：gprof 是"插桩+采样"的老工具，跨平台不可靠；要找热点，先用 perf。**

**路线 B：插桩计时（成功，得到可用的实测占比）**

复制一份 `pivot_timed.c`（**算法与输出完全不动**，只在 `SumDistance` 里加了三段 `gettimeofday`），用 `-O2` 跑一次：

```
Using time : 37200.642000 ms
[INSTR] SumDistance calls = 124750
[INSTR] rebuild coords   =     3076.1 ms  ( 8.30 %)
[INSTR] chebyshev sum    =    33952.7 ms  (91.65 %)
[INSTR] malloc           =       17.0 ms  ( 0.05 %)
[INSTR] accounted total  =    37045.8 ms
```

原始输出见 `data/hotspot-instrumented-local.txt`，插桩源码见 `data/pivot_timed.c`；这次运行 `result.txt` 仍然是 `924858624d0290f1`（与 refer 一致），**证明插桩没有改变行为**。

**这三行数字说明什么**：

1. `SumDistance` 被调用 **124750 次** = `C(500,2)`，与"枚举所有组合"完全吻合；
2. **91.65% 的时间在切比雪夫双重循环**（`n²·k` = 50 万次比较/组），只有 8.30% 在重建坐标（`n·k·dim`）；
3. `malloc` 只占 **0.05%**（124750 次 8 KB 分配，fastbin 级别）——所以"12 万次 malloc"听着吓人，实测**根本不是瓶颈**；这正好说明为什么不能靠直觉猜热点；
4. 三段合计 37.05 s / 总 37.20 s = **99.6%**，剩下 0.4% 才是排序 + 迭代 `printf` + 递归开销。

**但它给不出什么**：插桩只能测"我事先认为该测的段落"，测不出 IPC、cache-misses、branch-misses，也不能发现"我没预料到的热点"（比如 libc 里的 `printf`/`malloc` 内部）。**这正是必须上 Linux 服务器跑 perf 的原因**——`perf stat` 给体质数据，`perf record` 给无偏热点，两者和上面的插桩结论互相印证时，结论才可信。

**路线 C：ETW 采样（备选，未采用）**：`wpr -start CPU` → 跑程序 → `wpr -stop` → `xperf -i trace.etl -a dumper -profile` 也能给出函数级采样；但 mingw 产物没有 PDB 符号，`xperf` 只能显示"模块 + 偏移"，对我们的源码级热点判断价值有限，故未展开。
