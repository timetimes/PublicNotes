# $\LaTeX$

$\LaTeX$ 是一种基于ΤΕΧ的排版系统，由美国计算机学家莱斯利·兰伯特（Leslie Lamport）在20世纪80年代初期开发，利用这种格式，即使使用者没有排版和程序设计的知识也可以充分发挥由TeX所提供的强大功能，能在几天，甚至几小时内生成很多具有书籍质量的印刷品。对于生成复杂表格和数学公式，这一点表现得尤为突出。因此它非常适用于生成高印刷质量的科技和数学类文档。

## 语法

注释%
命令/

需要转义（用/）的特殊符号:%、&、$、~、^、_、{、}、#

设定区域
\documentclass{}
\usepackage{}
规定论文格式，导入相关依赖包

正文区域
\begin{}
\end{}
可见内容

正文各级标题

`\\`换行
`\par`换段
`\newpage`换页
`\setlength`首行缩进

数学公式
`$公式$`

```w
\begin{equation}\label{标签}
    公式
\end{equation}
```

`\[公式\]` 或 `$$公式$$`

依赖包amsmath
多行公式，分类

### begin

align 公式居中且左对齐，自动编号
align* 公式居中且左对齐，省略掉公式后的编号
----matix----

enumerate 枚举类型

## 编译器

主要有MikTeX和Tex Live两款latex发行版，它们有些许的差别但前者支持使用时安装而不需要下载完整的tex包

MikTeX + VS Code 配置

1. * 安装[MikTeX](https://miktex.org/download)：下载安装，注意安装路径中不要包含中文，然后将...\miktex\bin\x64目录添加进用户环境变量
   使用控制台`...\miktex\bin\x64\miktex-console.exe`更新或下载宏包（因为加了环境变量，可以win+r输入miktex-console.exe打开，当然也可以在开始菜单或文件位置直接打开）
   * 安装[perl](https://strawberryperl.com/)：下载最新版本的msi安装文件安装即可，然后将...\Strawberry\perl\bin目录添加进用户环境变量
   * 在vscode中安装Latex-workshop插件
2. 随便创建一个.tex文件
   左侧栏中找到TEX按钮，点击Recipe:latexmk，就可以执行编译（直接点运行也可以）
   在当前目录下就可以找到对应输出的pdf
3. 在vscode的setting.json里添加一些额外配置。包括自动编译、自动清理等等。
   `"latex-workshop.latex.autoBuild.run": "never",`
   `"latex-workshop.view.pdf.viewer": "tab",`
   `"latex-workshop.latex.autoClean.run": "onBuilt"`
