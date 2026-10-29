# W02 · 林桂均（lgj）本周说明

## 一、本周做了什么

**主项：用 teach skill 学完「在 Linux 上跑通一个程序」主题（3 课时）**

在自己的 Mac 上给 AI 助手手工安装了 mattpocock/skills 仓库的 teach 技能（git clone 到临时目录 → 拷贝进 `~/.workbuddy/skills/` → 写 `~/.zshrc` 更新函数），然后用它系统学了一个 Linux 基础主题：

1. **第 1 课 · 编译四阶段流水线**：hello.c → 预处理(hello.i) → 编译(hello.s) → 汇编(hello.o) → 链接(hello)，在 Mac 终端亲手逐阶段跑通；理解了 `./程序` 与 PATH 的关系、执行位（chmod -x/+x）、退出码。
2. **第 2 课 · 依赖与环境**：缺依赖的三个时刻（编译期缺头文件 / 链接期缺实现 / 运行期缺动态库）、动态库搜索、环境变量 PATH、权限数字（644/755/umask）。
3. **第 3 课 · 真 Linux 首跑**：SSH 登录实验室服务器（hzcu-hpct，Ubuntu 22.04，gcc 12.3），同一份 C 代码不改一字跑通，对比 Mac 与 Linux 的差异（Mach-O vs ELF、libSystem vs glibc、otool -L vs ldd），并用 `dpkg -S` 反查了库的归属包。

**产出物**：课程课件存档、排查清单参考卡、学习记录（本地工作区 `~/WorkBuddy/teach-linux/`，后续整理后开源）。

**仓库链接**：[Judy7-coder/c_wedding](https://github.com/Judy7-coder/c_wedding) —— 上周完成的第一个完整 C 程序（新婚快乐动画）。

**AI 帮了什么忙（诚实分工）**

- teach skill 的安装、`~/.zshrc` 配置、`teach-update` 函数：我亲手执行，AI 只提供整行命令和机制讲解（有一步 AI 说写好了配置其实没写，被 cp 报错当场抓包——报错信息即真相）。
- 三节课：AI 讲机制、给命令；**所有命令由我本人在终端执行**，输出截图回报，AI 逐条判卷。
- 本文档：AI 起草骨架，我修改定稿。

## 二、学到了什么

**机制层面（最能复用的）**

- 编译四阶段每一步的中间产物都看得见：`file` 对 .i/.o/可执行给出三种指纹；736 字节的 .o 链接成 33KB 的可执行，差值就是从库里搬来的代码。
- **编译通过 ≠ 能跑**：缺依赖分三个时刻，报错长相完全不同——`fatal error: 'xxx.h' file not found`（编译期）、`undefined reference to 'xxx'`（链接期）、`error while loading shared libraries`（运行期）。
- 退出码是排错入口：`echo $?` → 0 成功、126 找到但不可执行、127 命令没找到。126 和 127 的区分能直接判断「权限问题还是路径问题」。
- **版本决定行为**：教科书说 `gcc` 编译 `sqrt()` 必须加 `-lm`，但 Ubuntu 22.04 的 glibc 2.35 已把数学函数并入 libc，不加也能过——遇到「说好会炸但没炸」，先查版本。
- Mac 与 Linux 的可移植性边界：C 源码可移植，产物（Mach-O/ELF）和运行环境（libSystem/glibc）不可移植。

**工作流层面**

- 报错的第一反应不是重跑，是 `cat -n 文件名` 对着报错行号看现场。第一报错是真的，后面多半是雪崩。
- Git 两段式：`add` 圈定暂存范围 → `commit` 本地快照 → `push` 上传远程。三者是三道独立的门，push 之前 GitHub 什么都不知道。
- PR 的本质：不是「拉取」，是「请求对方把我的分支合并进上游」，自带逐行 diff 和讨论区。

## 三、如何维护 / 更新自己的 GitHub 账号

- **小步提交**：一次 commit 只做一件事，commit 信息写清楚做了什么（`W02: lgj weekly notes` 这种格式），回溯时有账可查。
- **README 即门面**：每个仓库写清用途和用法，三个月后的自己也是读者。
- **SSH key 是主通道**：`~/.ssh/config` 给常用机器起别名（如 `Host lab`），密钥权限保持 600。
- **保持活跃**：学到的产出整理后 push 到自己仓库，让提交记录成为学习史。

## 四、如何给别人的仓库做贡献

1. **没有写权限时**：Fork（网页复制到自己账号）→ clone 自己的副本 → 开分支 → 改动 → push 到副本 → 向上游发 PR。
2. **有写权限时**（本次）：直接在组织仓库开分支（`W02-lgj`）→ 改动 → push → 发 PR，省掉 Fork 一层。
3. **PR 礼仪**：标题和描述写清「改了什么、为什么」；reviewer 留言后改完再 push 到同一分支，PR 自动更新；被要求改动不等于被否定，diff 视图就是给人挑毛病的。
