---
date : '2025-02-26T00:11:50+08:00'
draft : False
title : 'LaTeX学习'
image : https://raw.githubusercontent.com/Shigtora/my_blog_img/main/2.jpg
categories : 
  技能
---

## 1. 引言 ##
### 1.1 什么是LaTeX ###
  **LaTeX**‌是一种基于ΤΕΧ的排版系统，与大众普遍使用的Word等*所见即所得*的文档编排工具不同,LaTeX是采用*所想即所得*的写作逻辑，用户通过LaTeX语言描述内容结构，由编译器生成精美的PDF文本。

### 1.2 为什么要使用LaTeX ###
* **数学公式**：支持多行对齐、矩阵等复杂公式。
- **引用管理**：自动生成文献目录与编号。
* **跨平台一致性**：编译后的 PDF 在任何设备上显示效果一致。
* **适用于Word**：Word支持LaTeX语法输入。
* **丰富的插件**：通过插件可以写化学方程式、绘制图像等。
## 2. 编辑器推荐 ##
* Obsidian：首推，支持Markdown语法
* Vscode ＋ LaTeX插件
* Overleaf：在线工具，随开随用，有精美的主题（官网：[overleaf.com](https://www.overleaf.com/)）

## 3. 语法查询网站 ##
* https://katex.org/docs/supported.html
* https://coffeetea.top/zh/markdown/Formula.html

## 4. 语法展示 ##
* 简单语法展示：
| 符号     | 代码           |
| ------ | ------------ |
| 希腊字母 α | \alpha       |
| 积分 ∫   | \int_{a}^{b} |
| 矢量箭头 → | \vec{v}      |

* 创建一个矩阵

$$
\begin{pmatrix}
1&a_1&a_1^2&\cdots&a_1^n\\
1&a_2&a_2^2&\cdots&a_2^n\\
\vdots&\vdots&\vdots&\ddots&\vdots\\
1&a_m&a_m^2&\cdots&a_m^n\\
\end{pmatrix}
$$
```LaTeX
$$
\begin{pmatrix}
1&a_1&a_1^2&\cdots&a_1^n\\
1&a_2&a_2^2&\cdots&a_2^n\\
\vdots&\vdots&\vdots&\ddots&\vdots\\
1&a_m&a_m^2&\cdots&a_m^n\\
\end{pmatrix}
$$
```

* 求解一个不定积分
$$
\int{\frac{arctan^2x}{(x+arctanx)^2}}
$$
```LaTeX
$$
\int{\frac{arctan^2x}{(x+arctanx)^2}}
$$
```

* 写一个化学方程式
$$
CH_2=CH_2 + Cl_2 \rightarrow ClH_2C-CH2Cl
$$
```LaTeX
$$
CH_2=CH_2 + Cl_2 \rightarrow ClH_2C-CH2Cl
$$
```

* 定积分定义
$$
\lim_{n \to \infty}
\displaystyle\sum_{i=1}^n
f[a+\frac{i}{n}(b-a)]
\frac{b-a}{n}
=
\int_a^b f(x)
$$
```LaTeX
$$
\lim_{n \to \infty}
\displaystyle\sum_{i=1}^n
f[a+\frac{i}{n}(b-a)]
\frac{b-a}{n}=\int_a^b f(x)
$$
```