# 学生名单 · Roster

**HZCU HPC Team** 2026 秋季学期

## 成员

| 缩写 | 姓名 | 目录示例 |
|---|---|---|
| `jy` |姜杨 | `W01/jy/` |
| `wyt` | 汪予甜 | `W01/wyt/` |
| `whh` | 王厚骅 | `W01/whh/` |
| `wcy` | 翁楚越 | `W01/wcy/` |
| `lgj` | 林桂均 | `W01/lgj/` |
| `cyl` | 陈亚亮 | `W01/cyl/` |
| `cyp` | 蔡源培 | `W01/cyp/` |

## 命名规则

- 缩写取**姓名拼音首字母**，全小写
- 每周每位同学一个文件夹：`W<周次>/<缩写>/`
- 文件夹与文件名一律用英文，不出现中文
- 目录名、文件名统一小写，多个词用连字符连接：`slides-draft-20261018.pptx`

## 提交方式

在自己的目录下提交时：

```bash
git pull                      # 先同步远端
# 把自己的文件放进W01/<缩写>/
git add W01/<缩写>/
git commit -m "W01: add literature review"
git push
```

更推荐走 Pull Request，理由见主 [README](README.md)。