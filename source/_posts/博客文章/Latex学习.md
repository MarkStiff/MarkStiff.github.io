---
title: Latex基本操作
date: 2022-10-4 21:13:29
tags: 
	- Latex
cover: https://cdn.jsdelivr.net/gh/LZHMS/picx-images-hosting@master/ZBlog/Covers/wp10372759-winter-cozy-desktop-wallpapers.50onb01lglc0.webp
toc: true
categories: 博客文章
excerpt: 关于Latex基本操作学习.
---
### Latex学习一————基本结构

#### 1.1 主体结构

源程序分为导言区和正文区，其中导言区设置文章的一些性质或自定义命令，选定文档类命令为 `\documentclass{article}`，设置文章属性可以加入命令 `\title{}`,`\auther{}`,`\date{}`
正文区又称文稿区，设置文档环境命令 `\begin{document}`,`\end{document}`,一篇文档有且只能设置一个文档环境。

#### 1.2 部分命令

```Latex
\maketitle % 生成标题，用在`book/report/article`类的正文区中，而`letter`类在正文区并没有此命令。              
$ $  % 单`$`命令主要用于行内公式书写   
$$ $$ % 而双`$$`命令用于行间公式  
\tableofcontents  % 输出文章目录   
\bibliographystyle   % 声明参考文献的格式   
\footnote{}   % 在正文后面设置脚注，花括号内的部分是命令的参数，即脚注的内容。   
\emph{}  % 改变字体形状，表示强调(emphasis)的内容   
\begin{quote}
% 将环境中的内容单独分行，增加缩进和上下间距排印，以突出引用的部分。
% 同时设置引用的字体
\zihao{-5}\kaishu   % 设置字号和字体命令  会影响后面所有文字(环境内)
% 注：\zihao{}有参数，-5即小五号
\end{quote}
\begin{abstract}
文章摘要环境，在\maketitle之后设置
\end{abstract}
```

例：

```Latex
% 导言区
\documentclass{article}    % book,report,letter

\title{My First Document}
\author{MarkStiff}
\date{\today}

% 正文区(文稿区)
\begin{document}
	\maketitle
	Hello World!

	% here is my big formula
	Let $f(x)$ be defined by the formula $$f(x)=3x^2+x-1$$ which is a polynomial of degree 2.
\end{document}
```

生成效果图:
![](https://ms-blogimage.oss-cn-chengdu.aliyuncs.com/picture/img/1.png)

### Latex学习二————中文文档设置

#### 2.1 文档整体设置

+ 可以加入 `\usepackage{ctex}`命令使用扩展包；
+ 直接设置整体文档类 `\documentclass[UTF8]{ctexart}`,此外还有 `ctexbook ctexrep`

可选参数表明中文文档的编码，主要有 `GBK和UTF8`，不同 `Latex`编辑器默认编码方式不同。

#### 2.2 `equation`环境

```latex
\begin{equation}
AB^2 = BC^2 + AC^2.
\end{equation}
```

此环境命令主要是用于产生带编号的行间公式。

#### 2.4 章节设置

`\section{章节标题}`生成一节的标题

#### 2.3 中文字体设置

##### 字体族设置

——罗马字体、无衬线字体、打字机字体

+ 字体命令

```Latex
\textrm{文本} % 设置字体族为罗马字体
\textsf{文本}  % 无衬线字体
\texttt{文本}  % 打字机字体
```

+ 字体声明命令

```Latex
\rmfamily 文本    % 声明以后的字体使用罗马字体
\sffamily 文本 % 无衬线字体
\ttfamily 文本  % 打字机字体
{\rmfamily 文本}  % 使用括号限定字体声明范围
```

##### 字体系列设置

```
 Pass
```

### Latex学习三———— 杂谈

#### 3.1 定理环境

文章定理之类的是用一类定理环境输出的，在使用之前需要在导言区做定义:
`\newtheorem{thm}{定理}`
定理环境有一个指定定理名字的可选参数，示例:

```Latex
\begin{thm}[勾股定理]
直角三角形斜边的平方等于两腰的平方和。

可以用符号语言表述为······
起源于6--7年份  % 表示数字范围时可以用两个减号来输出Latex中的短横线
\end{thm}
```

#### 3.2 数学公式

```Latex
% 行间公式 行内公式 pass
\angle ACB = \pi/2    % 角符号以及使用pi命令
f_pump   % '_' 命令下标设置
f^2      % '^' 命令上标设置
% 注：如果上下标不止一个符号则需要用花括号进行分组
90^\circ   % 设置角度上标
```

实际效果如图:
![](https://ms-blogimage.oss-cn-chengdu.aliyuncs.com/picture/img/20221006213148.png)

#### 3.3 使用图表

+ 插图功能
  插图功能由 `graphicx`宏包提供，需要在导言区进行设置
  `		 \usepackage{graphicx}`
  具体的插图命令为：
  `		 \includegraphics[width=3cm]{xiantu.pdf}`
  其中可选参数设置图片在文档中的宽度，第二个参数是图形的文件名（放在源文件所在目录）
  使用xelatex命令编译时，支持的图形格式包括PDF、PNG、JPG、FPS等
  **_图形放置_**
  通常将图像放置在一个浮动体中，处于一个可以变动相对位置的环境中

```Latex
\begin{figure}[ht]    % 设置浮动体环境
	\centering   % 表示后面的内容居中
	\includegraphics[scale=0.6]{cover.jpg}
	\caption{博客封面设计图} % 给插图加自动编号和标题
	\label{fig:封面图}  % 设置插图标签
\end{figure}
```

注：可选参数 `ht`表示浮动体可以出现在环境周围的文本所在处(`here`)和一页的底部(`top`)
具体效果图如下：
![](https://ms-blogimage.oss-cn-chengdu.aliyuncs.com/picture/img/202210071411539.png)

+ 制作表格
  设置表格环境 `tabular`：

```Latex
\begin{tabular}{|rrr|}
	\hline
	直角边 $a$ & 直角边 $b$ & 斜边  $c$ \\
	\hline
		3 &   4 & 5\\
	\hline
		5 &   12 &   13\\
	\hline
\end{tabular}
```

注：

+ 可选参数 `|rrr|`表示表格有三列，都是右对齐，行与行之间用 `\\`隔开，列于列之间用 `&`隔开，表格中的横线用 `\hline`绘制
+ 表格环境设置，一般表格也放置在浮动体中，即 `table`环境

```Latex
\usepackage{float}
\begin{table}[H] % 使用H参数表示设置表格不浮动，需要在导言区添加float宏包
\begin{tabular}{|lll|}
	\hline
	直角边 $a$ & 直角边 $b$ & 斜边  $c$ \\
	\hline
	3 &   4 & 5\\
	\hline
	5 &   12 &   13\\
	\hline
\end{tabular}%
\qquad  % 此命令可以产生两个M宽度的空格
($a^2 + b^2 = c^2$)
\end{table}   
```

效果图:
![](https://ms-blogimage.oss-cn-chengdu.aliyuncs.com/picture/img/202210071412672.png)

#### 3.4 图表引用

+ 图片引用
  根据上文插图设置的标签属性可以很容易引用图片一个示例：`图\ref{fig:xiantu}是我国古代对勾股定理的一种证明`。
+ 公式引用
  公式添加标签示例:

```Latex
\begin{equation}\label{eq:gougu}   % 设定公式标签名
AB^2 = BC^2 + AC^2
\end{equation}
```

在正文中引用示例: `(\ref{eq:gougu})`注意公式引用的括号要手动添加
另解，使用宏包 `amsmath`,在导言区添加宏包，之后通过命令 `\eqref{eq:gougu}`引用，并能自动产生括号

#### 3.5 设计文章格式

一般设置文章整体格式可以借用宏包直接进行处理，现列举较为常用的文章格式宏包:

```Latex
\usepackage{gemetry}   % 设计页面尺寸宏包
\geometry{a4paper,centering,scale=0.8}  % 定义A4纸大小，版心居中，宽0.8倍

\usepackage[format=hang,font=small,texfont=it]{caption}   % 改变图表标题格式
% 设定图表标题悬挂对齐，整体用小字号，标题文本使用斜体（对汉字而言是楷书）
\usepackage[nottoc]{tocbibind}  % 增加目录的项目
% 宏包默认会在目录中加入目录项本身、参考文献、索引等项目，这里使用nottoc选项取消了在目录中显示目录本身
```

**_自定义环境_**
如果需要设置特定的段落环境，可以利用已有的环境在导言区构造新的环境，以达到增加格式控制的目的

```Latex
% 这里对引用(quote)环境重新设置，增加更多格式控制命令
\newenvironment{myquote}
	{\begin{quote}\kaishu\zihao{-5}}
	{\end{quote}}
% 这里新环境由环境名字、环境开始代码和环境末尾代码三个参数，这样在导言区定义可以重复使用
% 使用
\begin{myquote}
text······
\end{myquote}
```

**_自定义命令_**
在一些需要的地方，`Latex`给我们提供了自定义新的命令的代码，这极大地拓展了不同背景和领域使用的便利性。

```Latex
% 这里以角度上标为例
\newcommand\degree{^\circ}      % 在导言区定义
$90\degree$ = $90^\circ$  
```

插图版式调整后效果:
![](https://ms-blogimage.oss-cn-chengdu.aliyuncs.com/picture/img/202210071440767.png)
