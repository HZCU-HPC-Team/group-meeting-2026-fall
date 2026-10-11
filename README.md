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
├── .gitignore
├── W01/
│   ├── this-week.md           # 讲师：本周讲了什么
│   ├── next-week-tasks.md     # 讲师：下周要完成什么
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

## 两条线

每周文件夹里有两类内容：

**讲师侧** —— `this-week.md` 记录本次组会讨论了什么，`next-week-tasks.md` 布置下次之前要完成的任务。
每周只追加、不改写既往记录；要改也是补新条目，不覆盖旧内容。

**学生侧** —— 每位同学在自己缩写命名的文件夹里放本周的作业、汇报材料、文献笔记等。
文件夹按「主题名-日期」命名，例如：

```
W01/jy/literature-review-20261015.pdf
W01/jy/slides-draft-20261018.pptx
```

两条线不交叉：讲师不写学生的个人目录，学生也不改讲师的两个 md 文件。变更通过提交信息留痕。

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
mkdir -p W11
git mv W10/this-week.md       W11/this-week.md
git mv W10/next-week-tasks.md W11/next-week-tasks.md

# 2. 把内容里的 W10 替换成 W11
sed -i "s/W10/W11/g" W11/this-week.md W11/next-week-tasks.md

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