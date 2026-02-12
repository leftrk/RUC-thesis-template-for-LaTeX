![image](https://user-images.githubusercontent.com/11362493/144565641-926c4828-1c56-486f-94cc-4b7d14afb3c8.png)

# 中国人民大学 LaTeX 论文模板 (RUC-Thesis)

这是一个适用于中国人民大学本科、硕士（学硕+专硕）和博士学位论文的 LaTeX 模板。

> 符合学校和老师的模板就是好模板，你需要仔细的考虑自己是否需要LaTeX，其实 Word 也是不错的软件。
> 临近毕业，发邮件提问的学弟学妹越来越多了，希望大家开[issue](https://github.com/GH1995/RUC-thesis-template-for-LaTeX/issues)讨论，或者直接发PR，这样可以帮助更多的人。

目前支持本科、硕士（学硕+专硕）和博士，排版出来的封面和下面差不多，可以在 [overleaf](https://www.overleaf.com/read/kmjxwrcjstqx) 上直接预览。

<img src="./figures/Snipaste_2020-06-17_03-55-47.png" height="500rem" alt="example" align=center />

## 1. 使用方法

本模板使用 `XeLaTeX` 作为排版引擎，因为它对中文支持最好。

### 环境准备

1.  **安装 TeX 发行版**：
    *   **MacOS**: 推荐安装 [MacTeX](https://www.tug.org/mactex/)。
    *   **Windows**: 推荐安装 [TeX Live](https://www.tug.org/texlive/) (不推荐 CTeX 套装)。
    *   **Linux (Ubuntu)**: `sudo apt install texlive-full`。
2.  **安装字体**：
    *   模板默认使用了 **方正小标宋简体** (FZXBSJW--GB1-0) 用于部分标题。
    *   您可能欠缺这部分字体，为此我们提供[这里（不是百度网盘）](https://ruc.lanzouo.com/inJo9xec09i)以供下载。下载后请安装到系统字体目录。

### 编译论文

#### 方法 A：使用 latexmk (推荐)

本项目已配置 `.latexmkrc`，支持自动化编译。如果您安装了 `latexmk`（通常包含在 TeX Live/MacTeX 中），只需在项目根目录下运行：

```bash
latexmk
```

它会自动处理 `xelatex` -> `bibtex` -> `xelatex` 的依赖关系，并生成 `main.pdf`。

清理中间文件：
```bash
latexmk -c
```

#### 方法 B：手动编译

如果您习惯手动编译，请严格按照以下顺序执行命令，以确保目录和参考文献正确生成：

```bash
xelatex main.tex
bibtex main
xelatex main.tex
xelatex main.tex
```

### 配置论文信息

打开 `main.tex` 文件，在导言区配置您的个人信息：

```latex
\documentclass[a4paper,bachelor]{ructhesis} % 选项: bachelor, master, doctor, promaster

...

\title{您的论文题目}
\author{您的姓名}
\school{您的学院}
...
```

*   **学位选项**：在 `\documentclass` 中选择 `bachelor` (本科), `master` (学硕), `promaster` (专硕), 或 `doctor` (博士)。
*   **正文内容**：正文章节放在 `chap/` 目录下，并在 `main.tex` 中通过 `\include` 引入。

## 2. 技术细节

### 核心文件

*   **`ructhesis.cls`**: 核心文档类文件，定义了论文的整体样式、页眉页脚、标题格式等。基于 `ctexbook` 文档类开发。
*   **`ref/rucbib.bst`**: 参考文献样式文件，基于 `gbt7714-2015` 标准修改，以符合人大论文规范。

### 宏包与依赖

本模板经过优化，移除了一些过时的宏包，采用了更现代的方案：

*   **排版引擎**: 必须使用 `XeLaTeX`，以支持 UTF-8 编码和系统字体调用。
*   **图表**: 使用 `graphicx` 处理插图，`booktabs` 处理三线表。
*   **子图/子表**: 使用现代的 `subcaption` 宏包，替代了过时的 `subfigure` 和 `caption2`。
*   **字体命令**: 更新了旧式的 `\bf`, `\rm` 等命令为 `\bfseries`, `\rmfamily` 等，符合 LaTeX2e 标准。

### 目录结构

*   `chap/`: 存放各章节的 `.tex` 源码。
*   `format/`: 存放摘要、致谢等固定格式页面的 `.tex` 源码。
*   `figures/`: 存放论文所需的图片文件。
*   `ref/`: 存放参考文献数据库 (`.bib`) 和样式文件 (`.bst`)。
*   `main.tex`: 主控文件，用于组织全文。

## 常见问题

*   **编译报错 "Font ... not found"**: 请检查是否安装了“方正小标宋简体”等字体。
*   **参考文献显示不出来**: 请确保运行了 `bibtex` 命令（或使用了 `latexmk`），并且 `.bib` 文件中有相应条目。
*   **Overleaf 使用**: 如果在 Overleaf 上使用，请将项目的编译器设置为 `XeLaTeX`。

---
![Alt](https://repobeats.axiom.co/api/embed/178d62098f91e5a8b1c3439855fa0ec5cae1f803.svg "Repobeats analytics image")
