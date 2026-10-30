# W03 · 蔡源培（cyp）

**本周作业：跑通赛题 → 编译优化 → perf 看热点**

> 说明文件按"做了什么 + 学到了什么 + 证据在哪"组织。所有数字都有对应的原始日志，链接写在各节里。

---

## 0. 结论速览

| 环节 | 状态 | 关键结果 |
|---|---|---|
| 1. 跑通赛题 | ✅ 完成（本机 gcc/mingw）；⏳ 服务器 hzcu-hpct 待复跑 | `result.txt` 与 `refer-2dim-5h.txt` **2000 行逐字节一致** |
| 2. 最小单位 | ✅ 完成 | 环境 → 源码 → 编译 → 链接 → 运行 → 输出，每一步都有验证命令 |
| 3. 编译优化实验 | ✅ 完成（本机） | `-O0 → -O3` 时间的量级差异见 [compile-opts.md](compile-opts.md)；换选项后结果不变 |
| 4. perf | ✅ 方案 + 脚本 + 本机插桩实测热点；⏳ PMU 计数器（cycles/instructions/cache/branch）待上服务器 | 本机实测：**99.6% 时间在 `SumDistance`**（切比雪夫求和 91.65% + 重建坐标 8.30% + malloc 0.05%），见 [perf.md](perf.md) 第 7 节 |
| 5. 说明文件 | ✅ 本文件 | 已在 `W03/cyp/` |

**一句话结论**：这道赛题 99% 的时间花在 `SumDistance()` 上——它每评估一组 pivots 就要重算 `n × k` 个重建坐标，再算 `n × n` 个点对的切比雪夫距离；总组合数 `C(n,k) = C(500,2) = 124750` 组，内层累计约 **6.24 × 10¹⁰** 次距离比较。所以"换编译选项"只是常数级改善，真正的加速必须从算法和数据复用上做（W04 再说）。

---

## 1. 我亲手做了什么（命令级记录）

完整逐条记录见 [run-log.md](run-log.md)，下面是骨架：

```bash
# 环境：先查有没有，再决定装不装
which gcc && gcc --version          # 已有 gcc，不需要装
lscpu | head -20                    # 机器什么规模
free -h                             # 内存够不够（本题 malloc 只有几十 KB，肯定够）

# 拿源码
tar -xf pivot.tar                   # 得到 pivot/ 目录：pivot.c + 输入 + refer

# 编译（先用参考命令，不加优化）
gcc pivot.c -lm -o pivot

# 运行（单次几十秒~几分钟，挂后台别让 SSH 断了）
nohup ./pivot uniformvector-2dim-5h.txt > run.log 2>&1 &

# 先对再快：结果和基准文件比对
diff result.txt refer-2dim-5h.txt && echo SAME
```

我本机没有 Linux，`perf` 不存在（见 [perf.md](perf.md) 第 1 节），所以 1~3 项先在 Windows + w64devkit gcc 16.2.0 上跑通并测数据；第 4 项 perf 的采集方案、脚本、记录表按 `hzcu-hpct`（Ubuntu 22.04 + Slurm，128 核）写死，登录后一条命令即可产出数据。

---

## 2. 我学到了什么

### 2.1 "跑通"不是一个动作，是一条链

以前觉得"跑通 = 程序没报错"。这次按 `环境 → 源码 → 编译 → 链接 → 运行 → 输出` 拆开，才发现每一环都能独立出错，而且**每一环都可以单独验证**：

- 环境错：`gcc` 没装 / 版本不对 → `gcc --version` 立刻暴露；
- 编译错：语法、头文件 → `-Wall` 加警告、逐个修；
- 链接错：`-lm` 漏了 → `undefined reference to pow/sqrt`，这是本题最常见的坑；
- 运行错：输入文件路径不对 → 程序自己打印 `uniformvector-2dim-5h.txt file not found.`；
- 输出错：算错了、或者格式不对 → `diff result.txt refer-*` 立刻判定。

细节见 [minimal-chain.md](minimal-chain.md)。

### 2.2 编译优化是"免费的加速"，但上限很明显

同一份代码、同一台机器，只改 `-O0/-O1/-O2/-O3`，时间就有数倍差距——因为编译器会做寄存器分配、循环不变量外提、`pow(x,2) → x*x`、向量化。但代价是**它一个字节的算法都不会替你改**：`C(n,k) × n²` 还是 `C(n,k) × n²`。所以编译选项 + `-march=native` 属于"第一次白捡"，之后必须动算法。

### 2.3 "先对再快"是纪律，不是口号

编译选项一换，浮点求和顺序可能变，数值就可能有末位差异。本周每次换选项我都重跑并 `diff`，确认 2000 行输出没变——**加速比只有在结果仍然正确时才有意义**。

### 2.4 perf 的价值：把"我觉得慢在 SumDistance"变成"数据说 99.x% 在这里"

靠读代码猜热点，容易猜错（尤其是 `malloc/free`、排序、IO 这些"看起来贵"的地方）。perf 的采样 + 硬件计数器把这件事变成可量化的：热点函数占比、IPC、cache/branch miss 率，直接告诉你"该往哪个方向改"——是算得太多（计算密集），还是内存喂不饱（访存密集）。详见 [perf.md](perf.md)。

---

## 3. 目录

```
W03/cyp/
├── README.md             # 本文件：结论 + 收获
├── run-log.md            # 亲手敲过的命令，逐条 + 每步在干什么
├── minimal-chain.md      # "最小单位"：源码→结果最少几步，每步怎么确认
├── compile-opts.md       # 编译优化实验：表格、加速比、diff 证据
├── perf.md               # perf：是什么 / 三件套 / 采集方案 / 记录表 / 怎么读
├── scripts/
│   ├── run-o-levels.sh   # 一键跑 -O0..-O3(+native)，每档 3 次，自动计时+存结果
│   ├── perf-stat.sh      # perf stat 采集（cycles/instructions/cache/branch）+ 自动算 IPC
│   ├── perf-record.sh    # perf record + report + annotate（找热点函数/行）
│   └── server-run-all.sh # 服务器上一键跑完上面全部（编译→计时→校验→perf）
└── data/
    ├── bench-local.txt               # 本机 6 档 × 3 次 原始日志
    ├── hotspot-instrumented-local.txt# 插桩实测热点原始输出
    ├── pivot_timed.c                 # 插桩版源码（算法不动，只加计时；用于自证 99.6%）
    └── perf-template.md              # 服务器采集回来的数据填这里
```

---

## 4. 下周要做

1. 在 `hzcu-hpct` 上把 [perf.md](perf.md) 的三条命令跑完，把数据填进 `data/perf-template.md`；
2. 把 perf 里的热点结论翻译成"改法清单"（复用重建坐标、去掉 `pow`、剪枝、并行化），W04 动手改。
