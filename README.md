# bigdata-ai-coursework

《大数据与人工智能》课程作业仓库。

## 目录结构

```
bigdata-ai-coursework/
├── assignments/   # 每次作业一个子目录，按 assignment-01、assignment-02 ... 命名
├── notes/         # 课程笔记与知识点整理
├── datasets/      # 作业用到的数据集（大文件不入库，见 .gitignore）
└── README.md
```

## 环境

- **Python 3.12.10**（仓库自带 `.venv`，见下方「开始使用」）
- Jupyter（已随 `.venv` 装好）／PySpark（按作业需要再装）
- **JDK 17.0.20.1**（Microsoft OpenJDK，PySpark 前置，`JAVA_HOME` 已配为机器级环境变量）
- Git 2.55.0

## 开始使用

**激活虚拟环境**（PowerShell / CMD，进仓库根目录后）：

```powershell
cd D:\wawa\bigdata-ai-coursework
.\.venv\Scripts\Activate.ps1
python --version        # 应输出 Python 3.12.10
```

> **坑 1**：若 PowerShell 报「无法加载文件 Activate.ps1，因为在此系统上禁止运行脚本」，先执行一次
> `Set-ExecutionPolicy -Scope CurrentUser RemoteSigned`，再激活。
> 不想改策略就用 CMD：`.\.venv\Scripts\activate.bat`

**`.venv` 丢了就重建**，注意**必须指定 3.12 的全路径**：

```powershell
& "C:\Users\sishi\AppData\Local\Programs\Python\Python312\python.exe" -m venv .venv
```

> **坑 2**：机器上另有一份 Python 3.13.12（其他工具在用，排在 PATH 前面）。
> 直接用 `python -m venv .venv` 会建出 3.13 的环境，依赖版本会和作业要求对不上。

**PySpark**：前置 JDK 已就绪。需要时再装：

```powershell
pip install pyspark
```

装完先验证一下 Java 能不能被找到：

```powershell
python -c "import pyspark; print(pyspark.__version__)"
```

> **坑 3**：若报 `JAVA_HOME is not set`，手动指定一次即可：
> `$env:JAVA_HOME = "C:\Program Files\Microsoft\jdk-17.0.20.101-hotspot"`
> 注意这台机器上的 JDK 是 **Microsoft OpenJDK**（`C:\Program Files\Microsoft\`），
> **不是** Eclipse Temurin —— 网上教程里给的 Adoptium 路径在这里是错的。
> 正常情况下 `JAVA_HOME` 已设为机器级环境变量，不需要这步。

## 提交规范

每次作业完成后提交一次，commit message 形如：

```
assignment-01: 完成数据清洗与词频统计
```

## 注意事项

**`.gitignore` 对数据文件的排除是全局的**，不限于 `datasets/`。
`*.csv`、`*.tsv`、`*.parquet`、`*.zip`、`*.json.gz` 等一律不入库 —— 也就是说，
即使把一个小 CSV 放进 `assignments/`，Git 也会**静默忽略**它，提交时不会报错，但文件不会进版本库。

提交前用这条命令确认某文件到底会不会被忽略：

```powershell
git check-ignore -v assignments\assignment-01\data.csv
```

有输出 = 被忽略了；确实要提交就加 `-f`：`git add -f assignments\assignment-01\data.csv`