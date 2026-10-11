# group-meeting-2026-fall

**HZCU HPC Team** 2026 秋季学期组会仓库。

本仓库只覆盖一个学期。下学期另建`group-meeting-2027-spring`，无需迁移或改名。

---

## 目录结构

仓库以「周」为根目录，每周一个 `Wxx` 文件夹：

```
group-meeting-2026-fall/
├── README.md                  # 本文件
├── ROSTER.md                  # 学生名单与缩写对照
├── WORKLOAD.md                # 讲师工作量学期汇总
├── .gitignore
├── W01/
│   ├── this-week.md           # 讲师：本周讲了什么
│   ├── next-week-tasks.md     # 讲师：下周要完成什么
│   ├── workload.md            # 讲师：本次会议时长与出勤（权威）
│   ├── instructor/            # 讲师专属
│   │   ├── plan.md            # 本周授课计划 + 备料预估
│   │   ├── SUMMARY.md         # 本周汇总视图
│   │   └── materials/         # 授课材料，形式自选
│   ├── jy/                    # 姜杨
│   ├── wyt/                   # 汪予甜
│   ├── whh/                   # 王厚骅
│   ├── wcy/                   # 翁楚越
│   ├── lgj/                   # 林桂均
│   ├── cyl/                   # 陈亚亮
│   └── cyp/                   # 蔡源培
├── W02/
│   └── ...同上
├── ...
└── W10/                       # 已预建 W01–W10
```

**命名规则**：所有文件夹和文件一律用英文，不出现中文；文档**内容**用中文。
目录和文件名统一小写连字符风格。

---

## 讲师侧

讲什么完全自由——讲 VS Code、讲 Linux、讲服务器连接都可以，形式也不限：
幻灯片、Markdown 文档、实机演示、HTML 页面都行。

**结构固定，内容自由**：讲什么由讲师决定，但每一步都落在同一套结构上，
这样不同周次之间才可比。

### 每周文件分工

| 文件 | 性质 | 内容 |
|---|---|---|
| `Wxx/workload.md` | **权威** | 会议时长、出勤情况 |
| `Wxx/instructor/plan.md` | **权威** | 本周授课计划、下次预告、备料预估 |
| `Wxx/instructor/SUMMARY.md` | 视图 | 从上述两个文件汇总，冲突时以原始记录为准 |
| `Wxx/instructor/materials/` | 材料 | 授课用PPT / 文档 / 演示，按需添加 |

### 材料命名

放在 `Wxx/instructor/materials/`，按 `w<周次>-<主题>-<类型>` 命名：

```
W01/instructor/materials/
├── w01-vscode-intro-slides.pptx
├── w01-linux-basics-notes.md
├── w01-ssh-demo/
└── w01-ide-tools-ref.pdf
```

大文件（>50 MB）走 GitHub Releases，这里只放链接。

---

## 学生侧

每位同学在自己缩写命名的文件夹里放本周的作业、汇报材料、文献笔记等。
命名用「主题名-日期」：

```
W01/jy/literature-review-20261015.pdf
W01/jy/slides-draft-20261018.pptx
```

讲师侧与学生侧不交叉：讲师不写学生的个人目录，学生不改讲师的 md 文件。
变更通过提交信息留痕。

---

## 关于工作量记录

**计量口径：只算会议时长**，即讲师实际到场参与组会的时间。备课、答疑、材料审阅
等会外投入不计入本口径，单独记录在 `instructor/plan.md` 的备料预估中，两者分开统计。

这个口径客观、难以夸大，但**低估会外的真实投入**。学期末`WORKLOAD.md` 里
两种数字都列出来，讨论时可自行选择口径。

**请注意本表的性质**：数据由讲师本人填写，仓库不提供技术验证。
git 提交时间戳可作参考，但提交时间不等于工作发生时间。**这是一份声明，不是证据。**
详见 [WORKLOAD.md](WORKLOAD.md) 的说明。

**单周记录没有价值，能加总才有。** 每周填写，学期末才能形成有效总量。

---

## 学生缩写对照

见 [ROSTER.md](ROSTER.md)。缩写为姓名拼音首字母，全小写。

---

## 周次编号

`W01`、`W02`……从 1 开始，两位零填充，与学期内第几次组会对应。

仓库已预建 W01–W10。开学后若实际次数超过 10 周，继续往后加即可。

---

## 新增一周

```bash
# 1. 复制上一周的讲师文件（git mv 能保留文件历史）
mkdir -p W11/instructor/materials
git mv W10/this-week.md               W11/this-week.md
git mv W10/next-week-tasks.md         W11/next-week-tasks.md
git mv W10/workload.md                W11/workload.md
git mv W10/instructor/plan.md         W11/instructor/plan.md
git mv W10/instructor/SUMMARY.md      W11/instructor/SUMMARY.md
touch W11/instructor/materials/.gitkeep

# 2. 把内容里的 W10 替换成 W11
sed -i "s/W10/W11/g" W11/*.md W11/instructor/*.md

# 3. 为每位学生建目录（.gitkeep 让空目录能被 git 跟踪）
for s in jy wyt whh wcy lgj cyl cyp; do mkdir -p W11/$s && touch W11/$s/.gitkeep; done

# 4. 提交
git add W11
git commit -m "Add W11"
```

用 `git mv` 而不是 `cp`，git 才能识别为重命名，历史跟着走。

---

## 提交规范

- 一次提交只做一件事，提交信息写清楚：改了哪一周、什么内容
- 讲师文件用英文写提交信息；内容本身用中文
- 单个文件建议不超过 50 MB
- 超大文件或需要长期留存的版本，放 GitHub Releases，不进 git 仓库

---

## 提交方式建议

同学提交自己目录时，建议走 **Pull Request** 而不是直接 push：

- 归属清晰——谁交的、什么时候交的，在历史里一目了然
- 避免多人同时改仓库造成合并冲突
- 讲师可以 review 后再合并

首次提交前请先 `git pull`，避免与远端脱节。