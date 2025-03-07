---
date : '2025-03-04T00:11:50+08:00'
draft : False
title : 'TikZ'
math: true
image : https://pic1.imgdb.cn/item/67c9745f066befcec6df1a71.jpg
categories: 
  - LaTeX
  - 工具
  - 科研
---
> [!TIP]
> 推荐在阅读本篇文章前先阅读[*"LaTeX介绍"*](https://shimyy.netlify.app/p/latex%E5%AD%A6%E4%B9%A0/)作为铺垫。
## 1. 引言 
在了解了$\LaTeX$的基础用法之后，我们可以使用LaTeX内置插件TikZ进行绘图，优化科研体验。

## 2. 配置TikZ环境 
### 2.1 Vscode+LaTeX插件 
打开[Visual Studio Code](https://code.visualstudio.com/)官网链接，根据自己电脑系统下载合适版本。
[![1.png](https://pic1.imgdb.cn/item/67c96480066befcec6df04e3.png)](https://pic1.imgdb.cn/item/67c96480066befcec6df04e3.png)

下载完毕后，打开Vscode，下载几个插件进行配置LaTeX环境。
[![2.png](https://pic1.imgdb.cn/item/67c96480066befcec6df04e4.png)](https://pic1.imgdb.cn/item/67c96480066befcec6df04e4.png)
[![3.png](https://pic1.imgdb.cn/item/67c9647f066befcec6df04d6.png)](https://pic1.imgdb.cn/item/67c9647f066befcec6df04d6.png)

下载完毕后，按住Ctrl+Shift+P显示所有命令，点击“打开用户设置”
[![4.png](https://pic1.imgdb.cn/item/67c9647f066befcec6df04d7.png)](https://pic1.imgdb.cn/item/67c9647f066befcec6df04d7.png)

将以下内容粘贴至其中：
```json
// 编译链配置

  
  // 当设置为"never"时，禁用了保存LaTeX文档时自动编译的功能。
  "latex-workshop.latex.autoBuild.run": "onSave",
  // 启用VS Code编辑器中的LaTeX文件右键菜单。
  "latex-workshop.showContextMenu": true,
  // 启用LaTeX Workshop的智能感知功能，包括代码自动完成、参数信息等。
  "latex-workshop.intellisense.package.enabled": true,
  // 禁用错误信息在编辑器中的显示。
  "latex-workshop.message.error.show": false,
  // 禁用警告信息在编辑器中的显示。
  "latex-workshop.message.warning.show": false,
  // 定义了LaTeX编译工具的配置，包括工具名称、命令和参数。
  
  "latex-workshop.latex.tools": [
    {

      "name": "xelatex", // 工具名称：xelatex

      "command": "xelatex", // 执行的命令

      "args": [ // 命令参数
        "-synctex=1", // 启用同步TeX，方便在PDF和源文件之间跳转
        "-interaction=nonstopmode", // 设置为非停止模式，编译时不中断
        "-file-line-error", // 显示错误的文件名和行号
        "%DOCFILE%" // 代表当前文档的路径
      ]
    },
    {
      "name": "pdflatex", // 工具名称：pdflatex
      "command": "pdflatex",
      "args": [ // 命令参数，与xelatex类似
        "-synctex=1",
        "-interaction=nonstopmode",
        "-file-line-error",
        "%DOCFILE%"
      ]
    },
    {
      "name": "latexmk", // 工具名称：latexmk
      "command": "latexmk",
      "args": [ // 命令参数，latexmk特有的参数
        "-synctex=1",
        "-interaction=nonstopmode",
        "-file-line-error",
        "-pdf", // 生成PDF输出
        "-outdir=%OUTDIR%", // 输出目录，%OUTDIR%为占位符
        "%DOCFILE%"
      ]
    },
    {
      "name": "bibtex", // 工具名称：bibtex
      "command": "bibtex",
      "args": [ // 命令参数
        "%DOCFILE%" // 代表当前文档的路径，用于处理参考文献
      ]
    }
  ],
  // 定义了LaTeX编译流程的名称和使用的编译工具序列。
  "latex-workshop.latex.recipes": [
    {
      "name": "XeLaTeX", // 编译流程名称：单独使用XeLaTeX
      "tools": ["xelatex"] // 使用的工具
    },
    {
      "name": "PDFLaTeX", // 编译流程名称：单独使用PDFLaTeX
      "tools": ["pdflatex"]
    },
    {
      "name": "BibTeX", // 编译流程名称：单独使用BibTeX
      "tools": ["bibtex"]
    },
    {
      "name": "LaTeXmk", // 编译流程名称：使用latexmk
      "tools": ["latexmk"]
    },
    {
      "name": "xelatex -> bibtex -> xelatex*2", // 编译流程名称：xelatex + bibtex + 两次xelatex
      "tools": ["xelatex", "bibtex", "xelatex", "xelatex"]
    },
    {
      "name": "pdflatex -> bibtex -> pdflatex*2", // 编译流程名称：pdflatex + bibtex + 两次pdflatex
      "tools": ["pdflatex", "bibtex", "pdflatex", "pdflatex"]
    }
  ],
  // 定义了编译过程中生成的临时文件类型，这些文件在清理时会被删除。
  "latex-workshop.latex.clean.fileTypes": [
    "*.aux", "*.bbl", "*.blg", "*.idx", "*.ind", "*.lof", "*.lot",
    "*.out", "*.toc", "*.acn", "*.acr", "*.alg", "*.glg", "*.gls",
    "*.glo", "*.ist", "*.fls", "*.log", "*.fdb_latexmk"
    // 这些文件类型包含了LaTeX编译过程中生成的各种辅助文件
  ],

  // 设置在编译失败时自动清理临时文件。
  "latex-workshop.latex.autoClean.run": "onFailed",
  // 设置默认使用上次使用的编译流程。
  "latex-workshop.latex.recipe.default": "lastUsed",
  // 设置PDF查看器中同步TeX的快捷键为双击。
  "latex-workshop.view.pdf.internal.synctex.keybinding": "double-click"
}
```

### 2.2 Overleaf在线编辑
>[!TIP]
>可以免费试用，后续使用需要会员。

使用[Overleaf](https://www.overleaf.com/)在线编辑，点击Templates选择合适的模板进行编辑即可。

## 3. TikZ基础语法 
>[!NOTE]
>以下均在Vscode环境下进行演示。
接下来用以下代码为例进行讲解基础代码说明。
```LaTeX
\documentclass{ctexart}
\usepackage{amsmath, mathrsfs, amsfonts}
\usepackage{tikz}
\usepackage{graphicx}
%引入几个宏包作为环境

\begin{document} %文件编写区
\begin{figure}[htp] %图标浮动形式htp
    \centering %图片居中
\begin{tikzpicture}[>=latex] 
%插入tikz图片，绘图区

    \draw[->] (-5,0)--(5,0) node[right] {$x$}; 
    %绘制从(-5,0)到(5,0)的带箭头的直线，坐标名称为x
    \draw[->] (0,-5)--(0,5) node[above] {$f(x)$};
    %绘制从(0,-5)到(0,5)的带箭头的直线，坐标名称为f(x)
  
\end{tikzpicture}
    \caption{}
\end{figure}

\end{document}
```
效果图：
[![5.png](https://pic1.imgdb.cn/item/67c9647f066befcec6df04d9.png)](https://pic1.imgdb.cn/item/67c9647f066befcec6df04d9.png)

## 4. 更多效果展示 
在学习了更多的TikZ语法后，通过在绘图区进行代码编写，我们可以绘制出如下精美的图片。

### 4.1 函数图像 
[![6.png](https://pic1.imgdb.cn/item/67c9647f066befcec6df04db.png)](https://pic1.imgdb.cn/item/67c9647f066befcec6df04db.png)
```LaTeX
\documentclass{ctexart}
\usepackage{amsmath, mathrsfs, amsfonts}
\usepackage{tikz}
\usepackage{graphicx}

\begin{document}
  \begin{tikzpicture}[domain=0:4]
    \draw[very thin,color=gray] (-0.1,-1.1) grid (3.9,3.9);
    \draw[->] (-0.2,0) -- (4.2,0) node[right] {$x$};
    \draw[->] (0,-1.2) -- (0,4.2) node[above] {$f(x)$};
    \draw[color=red]    plot (\x,\x)             node[right] {$f(x) =x$};
    \draw[color=blue]   plot (\x,{sin(\x r)})    node[right] {$f(x) = \sin x$};
    \draw[color=orange] plot (\x,{0.05*exp(\x)}) node[right] {$f(x) = \frac{1}{20} \mathrm e^x$};
    
  \end{tikzpicture}
\end{document}
```

### 4.2 3D图
[![7.png](https://pic1.imgdb.cn/item/67c9647f066befcec6df04dd.png)](https://pic1.imgdb.cn/item/67c9647f066befcec6df04dd.png)
```LaTeX
\documentclass{ctexart}
\usepackage{pgfplots}
\pgfplotsset{compat=1.16}

\begin{document}
\begin{tikzpicture}
\begin{axis}[colormap/viridis]
\addplot3[
    surf,
    samples=18,
    domain=-3:3
]
{exp(-x^2-y^2)*x};
\end{axis}
\end{tikzpicture}

\end{document}
```

### 4.3 电路图
[![9.png](https://pic1.imgdb.cn/item/67c96480066befcec6df04df.png)](https://pic1.imgdb.cn/item/67c96480066befcec6df04df.png)
```LaTeX
\documentclass{ctexart}
\usepackage{circuitikz}
\begin{document}

\begin{circuitikz}[american, voltage shift=0.5]
\draw (0,0)
to[isource, l=$I_0$, v=$V_0$] (0,3)
to[short, -*, i=$I_0$] (2,3)
to[R=$R_1$, i>_=$i_1$] (2,0) -- (0,0);
\draw (2,3) -- (4,3)
to[R=$R_2$, i>_=$i_2$]
(4,0) to[short, -*] (2,0);

\end{circuitikz}
\end{document}
```

### 4.4 化学有机式 
[![8.png](https://pic1.imgdb.cn/item/67c96480066befcec6df04de.png)](https://pic1.imgdb.cn/item/67c96480066befcec6df04de.png)
```LaTeX
\documentclass{ctexart}
\usepackage{chemfig}

\begin{document}

\chemfig{[:-90]HN(-[::-45](-[::-45]R)=[::+45]O)>[::+45]*4(-(=O)-N*5(-(<:(=[::-60]O)-[::+60]OH)-(<[::+0])(<:[::-108])-S>)--)}

\end{document}
```