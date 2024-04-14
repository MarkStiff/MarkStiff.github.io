---
title: Latex组织文本
date: 2022-10-07 14:50:49
tags:
    - Latex
cover: https://cdn.jsdelivr.net/gh/LZHMS/picx-images-hosting@master/ZBlog/Covers/wp13375902-cozy-book-wallpapers.7jo8z890l100.webp
toc: true
categories: 博客文章
excerpt: 关于Latex组织文本学习.
---
### 一、标点符号

#### 1.1 引号

`Latex`使用 `‘’`来表示引号，如果遇到连续使用单引号和双引号的情形，则需要使用 `\,`命令隔开，会产生很小的间距

#### 1.2 符号 `-`

+ 数学减号
+ 单独使用时表示连字符
+ 两个连用时，是 `en dash`，表示数字范围
+ 三个连用时，是 `em dash`，即破折号

`~`符号命令：数学模式 `$\sim$`

#### 1.3 省略号

西文省略号: `\ldots`或者 `\dots`，在句中使用时直接命令，而在句末使用时要把省略号放进数学模式中。
中文写作使用全角标点，一般由 `xsCJK`宏包控制，可以使用 `\punctstyle{}`命令修改，
![](https://ms-blogimage.oss-cn-chengdu.aliyuncs.com/picture/img/202211021153026.png)

#### 1.4 空格

以字母命名的宏后面空格会被自动忽略掉，此时可以使用 `\ `命令添加
或者添加一个空分组 `{}`分隔，或者 `{\TeX}`包裹进来
**不可打断的空格(带子)**
用 `~`表示，`function ~$f(x)$`
西方文体中，句末标点和缩写标点问题
`Latex`默认在大写字母的点看作缩写标记，小写字母后面的点看作句子结束而设置不同的点间隔；但当特殊情况时需要明确指定具体用法，示例:

```Latex
	Tinker et al.\ made the double play.  % '\空格'命令放在'.'后直接分隔单词

	Tinker et al,made the double play. % 一般情况下标点后需加空格

	\frenchspacing  % 禁止标点后的额外间距
	Roman number XII\@. Yes.  % '\@'命令放在'.'前面只处理'.'是句子结束点，之后再添加空格表示正常的句号标点
```

#### 1.5 幻影空格

```Latex
	% 幻影空格实际上起到占位作用，接受一个参数，生成与参数内容大小一样的空盒子
	% 类似的还有\hphantom和\vphantom表示水平竖直方向上的幻影
	MarkStiff\phantom{神奇}速速隐形

	MarkStiff神奇速速显形
```

#### 1.6 换行

```Latex
\\[2cm]  % 命令直接另起一行，上一行保持原样,可选参数设置换行后增加的额外垂直距离
\linebreak % 命令指定一行的断点，上一行仍按完整一行散开对齐
```

### 二、字体

#### 2.1 字体族格式命令

带参数命令主要用于少量字体的更换，三种字体族对应的带参数命令，而声明命令主要用偶遇分组或环境中字体的整体更换.

```Latex
带参数命令
	\textrm{Roman font family}
	\textsf{Sans serif font family}
	\texttt{Typewriter font family}

声明命令
	{\rmfamily Roman font family}
	{\sffamily Sans serif font family}
	{\ttfamily Typewriter font family}
```

效果图:
![](https://ms-blogimage.oss-cn-chengdu.aliyuncs.com/picture/img/202210071651052.png)

#### 2.2 字体形状命令

```Latex
带参数命令
	\textup{Upright shape}  % 直立形状
	\textit{Italic shape} % 意大利形状
	\textsl{Slanted shape} % 倾斜形状
	\textsc{SMALL CAPITALS SHAPE} % 小型大写形状

声明命令
	{\upshape Upright shape}
	{\itshape Italic shape}
	{\slshape Slanted shape}
	{\scshape SMALL CAPITALS SHAPE}
```

效果图：
![](https://ms-blogimage.oss-cn-chengdu.aliyuncs.com/picture/img/202210071650619.png)
倾斜形状一般是对符号直接倾斜产生的，而通常的“斜体”往往指意大利形状，数学公式的字体一般就使用意大利形状

#### 2.3 字体系列命令

```Latex
带参数命令
	\textmd{Medium series} % 中等字体，正文默认使用此系列
	\textbf{Bold extended series} % 加宽加粗

声明命令
	{\mdseries Medium series} 
	{\bfseries Bold extended series}
```

#### 2.4 字体坐标

经上文介绍了字体的三个特征，综合起来构成了确定一种字体的三维坐标：族、形状、系列，不同组合会产生不同的字体效果。
具体组合效果图:
![](https://ms-blogimage.oss-cn-chengdu.aliyuncs.com/picture/img/202210071702667.png)
**_恢复普通字体_**
在复杂的字体环境中，恢复普通字体就显得十分重要了。
`\textnormal{文字} % 带参数命令`
`{\normalfont 文字} % 声明命令`
**_斜体校正_**
在使用斜体声明 `\itshape、\slshape`时，最后一个倾斜的字体会超过右边界，使得间距过近；
而用带参数命令 `\textit、\textsl`时，可以自动修正这个距离，也可以手工使用 `\/`命令进行校正。
**_禁止校正_**
有时对于倾斜校正是不必要的，则应关闭带参数倾斜命令的自动校正功能:
`\textit{M\nocorr}M` 通过添加命令 `\nocorr`命令来关闭自动校正

#### 2.5 中文字体族

对于中文字体，一般只使用不同的字体族进行区分，选择中文字体族使用 `\CJKfamily`命令
在 `ctex`宏包及文档下有一些预定义，默认情况下配置了四种字体族：

```Latex
	{\heiti 这是黑体}
	{\songti 这是宋体}
	{\kaishu 这是楷书}
	{\fangsong 这是仿宋}
```

**_组合字体_**
`ctex`宏包及文档类也定义了一些组合字体，可以让中文也具备使用粗体和意大利体功能，并且重定义 `\rmfamily`使它同时对中文起作用
默认的中文字体是 `rm`，正常字体是宋体，粗体是黑体，意大利体是楷体
