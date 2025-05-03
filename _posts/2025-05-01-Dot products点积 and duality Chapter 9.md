---
layout: post
title: "2025-05-01 Dot products点积 and duality Chapter 9/16"
date: 2025-05-01
---

3Blue1Brown

**后记前置: 还挺沮丧的, 这个15min的视频, 我学了快三个小时. 从sc到lib的电脑屏幕前坐下, 已经3小时了** 不过看评论区说也有物理phd常看常新, 还有花了几小时才理解的comments, 给我安慰就是说我虽然笨还不是那么笨hh, 然后虽然要逃出和他人比较的逻辑, 但是我好像还是在这个体系中啊, 哎... 我觉得难的原因是(claude refine)
1. 教学视频受到时长限制，3Blue1Brown为了保持视频简洁，往往需要压缩内容，这就导致某些关键解释可能被简化或省略, 或者是被快速的讲解。
2. 作为斯坦福数学博士，Grant对数学概念的理解已经达到了非常深入的层次。这种专业洞察力有时会让他无意识的忽略初学者的思维盲区，使他在解释时跳过了对新手来说可能至关重要的中间步骤。
3. 一个视频需要面向不同水平的受众，从初学者到专业人士，这使得内容很难同时满足所有人的需求。

**2025-05-02记:** 又花了差不多4小时, 不过一半的时间在svg gpt作图上, 这个时候我想搭一个agent工具, or找找有没有现成的好的工具, 我觉得现在有的一个问题是现在LLM识别图像的能力非常非常弱, 我的截图对gpt输入, 让他使用svg来复刻, 基本无法识别, OK, 在打字的时候问题来了, 我输入一个png的截图, GPT是怎么读取的我的图片的, 这么短的时间内读取我的每一个像素点嘛, 不太可能, 应该还是Transformer 或者vit之类的, 我觉得我输入prompt如果是要求OCR识别的话, 好像都还蛮准的, 这里如果做agent的话, 要从原始目的出发研究一下. 或者说增强图片, 改变图片的分割方法. 为了减小文件体积, 和冗余, 文章尽量不使用任何png截图, 使整体md文档更加干净.

哎好失落啊, 这点东西配学这么久吗

**概念回顾**
什么是线性变换linear transformation, 核心的两个**形式性定义（formal properties）**，也叫**线性性公理**：
 ① **加法保持性（preservation of addition）**：

$$ L(\vec{v} + \vec{w}) = L(\vec{v}) + L(\vec{w}) $$

② **数乘保持性（preservation of scalar multiplication）**：

$$ L(c \vec{v}) = c \cdot L(\vec{v})$$


## 第一个有疑问的地方对于对称性, 我没有理解3Blue1Brown这里对于对称性的困惑

### 经过想之后的理解是

在一开始简单说了一下点乘的概念, 但是在2:17的时候, 说不对称, 没有理解这里不对称的意思, 其实是, 我们知道点乘是可以交换的, 但是这里交换后, 我们的几何意义改变了, 但是对于2维的vector点乘, 我们对于同样的对象(两个都是vector), 我们对于这个变化下, 其实两个vector的地位是不一样的, 一个是变化方, 一个是作为ground, 理论上我们交换位置, 这个formula应该会变好, 这里在几何意义上不同的object在交换后, 没有发生改变, 这里神奇的对称了. 顺序好像不重要了  

### GPT回复below

> 📌 **“这里说的不对称是说，两个向量，但是操作好像是不同的地位。”**

没错，作者用 “weirdly asymmetric（奇怪地不对称）” 来形容的，就是这种 **心理上的不对等感**，虽然实际上点积是数学上对称的操作。我们来把这个“不对称感”彻底拆清楚。 数学上：点积是对称的, 公式永远成立：

$$ \vec{v} \cdot \vec{w} = \vec{w} \cdot \vec{v}$$
这说明：
- 两个向量在**数学上的地位是完全一样的**；
- 交换它们顺序，计算结果不会变。
  
>但是几何解释上会让人感觉不一样

**让我们回顾那个几何解释的套路：**
把 $\vec{w}$ 投影到 $\vec{v}$ 所在的直线上，然后乘上 $|\vec{v}|$。这个解释其实默认了两件事：$\vec{v}$ 是被投影的参考方向，而 $\vec{w}$ 是主动参与投影的对象。它把两者的角色区分成了不同的几何意义：$\vec{v}$ 作为投影的目标、坐标轴和参考方向，而 $\vec{w}$ 则是被投影的向量和参与者。
所以你心里可能会产生这个疑问：为什么 $\vec{v}$ 是坐标轴一样的东西，而 $\vec{w}$ 是被压上去的？
如果你说："那我反过来，把 $\vec{v}$ 投影到 $\vec{w}$ 上，不也一样吗？"当然可以，而且你最终也会得到：$\vec{w} \cdot \vec{v} = \vec{v} \cdot \vec{w}$。但你会发现，这时候你投影的路径、过程完全不一样，虽然数值结果相等。就像你走了另一条路，但是到了同一个终点。
为什么这种"不对称"让人不舒服？因为我们习惯上会以为：如果两边平等，那解释方式也应该是平等的。但这里几何上的投影，总要选择一个方向来作为参考（轴），另一个投过去。这就导致你在心里赋予了一个向量"更高的地位"，这跟数学上的"完全对称"感觉不一致。这就是作者说的 "weirdly asymmetric" 的来源。


## 下面是看到一半时候, 我的疑惑(后来解决了)
后续在视频里面说, 如果 $\vec{v}$ 和 $\vec{w}$ 是本身对称的话, 这个投影的长度, 无论谁对谁, 好像值是不好变的, 然后如果改变一点的话, 比如,  $2\times \vec{v} \times \vec{w}$ 如果按照原来的理解的话,  $\vec{v}$ 变成了原来的两倍, 这个时候$\vec{w}$ 去逼近 $2\vec{v}$这个vector的话, 感觉应该值是不会变的, 因为对于ground vector来说, 肯定不可以影响阴影啊


# gpt回答... 使用Claude refine

上面的问题切中了**点积几何解释中投影与向量长度的关系**的核心。

你提出的疑问总结成一句话："我感觉点积是'影子长度'，那如果我把地面（ground vector）$\vec{v}$ 变长，比如变成 $2\vec{v}$，那影子的长度不应该变啊，因为地面变长不影响投影到它的'影子长度'——为什么点积的值却变了呢？"

这其实是一个常见直觉误区，也是这个视频中解释得最细致的地方。我们来用物理类比和直觉来破解这个问题：

先把点积的几何解释再说清楚：点积 = 投影长度 × 被投影方向的长度。也就是说：$\vec{v} \cdot \vec{w} = |\vec{v}| \cdot \text{(投影长度 of } \vec{w} \text{ onto } \vec{v})$。如果我们换个方式写：$\vec{v} \cdot \vec{w} = |\vec{v}| \cdot |\vec{w}| \cdot \cos\theta$，这里的意思是：你把 $\vec{w}$ 投影到 $\vec{v}$ 上（或反过来）；然后乘上 $\vec{v}$ 的长度（或 $\vec{w}$ 的长度）；得到一个带符号的投影值。

**类比一：投影 ≠ 影子**

你在想："如果我只是测影子长度，地板变长了（$\vec{v}$ 变成 $2\vec{v}$），影子不该变啊！"对！如果你只是测"影子长度"，确实不变。但问题是：点积不是"影子长度"，而是"影子长度 × 地板的长度"。

你可以把它类比成：力 × 位移 = 做的功（Work）。力 $\vec{F}$ 施加在一个方向；位移 $\vec{d}$ 在另一个方向；做功 = $\vec{F} \cdot \vec{d} = |\vec{F}||\vec{d}|\cos\theta$。如果你把 $\vec{F}$ 加大一倍，虽然 $\vec{d}$ 没有变，角度没有变，做功变成了两倍。因为你推得更用力了。

回到你的问题： 问题设定：原来：$\vec{v} \cdot \vec{w} = L$；现在我们改成：$2\vec{v} \cdot \vec{w} = ?$

发生了什么？投影长度（$\vec{w}$ onto $\vec{v}$）不变；但 $\vec{v}$ 自己的长度变成了两倍；所以最终点积值 = 原来的两倍！即：$2\vec{v} \cdot \vec{w} = 2 \cdot (\vec{v} \cdot \vec{w}) = 2L$。这不奇怪，因为你换了"参考线"：你不是只测"影子的长度"，而是"影子长度 × 地板的长度"，自然会变大！

类比二：放大尺子 想象你用尺子测一个影子长度。这个"尺子"就是 $\vec{v}$：原来：尺子是 1 米；你投影 $\vec{w}$，影子是 0.7 米；点积 = 0.7。你把尺子放大两倍：尺子变成 2 米；同样的影子 0.7 "尺"，但现在 1 尺 = 2 米，所以：点积 = 1.4。因为你改变了参考系！

总结你说的非常核心的一点：点积确实是关于"投影"的操作，但它还乘了个"参考向量的长度"，所以当你改变参考（地板）的时候，值当然会变。不能把点积误认为是"单纯的影子长度"——它其实是"影子 × 标尺的大小"。


## 继续

视频中的另外一个疑问(是作者本身的提问), 我之前没有注意到这个问题, 为什么下面这个形式, 乘以对并将它们相加的数值过程与投影有关？
$$
\begin{bmatrix} 2 \\ 7 \\ 1 \\ \end{bmatrix} \cdot \begin{bmatrix} 8 \\ 2 \\ 8 \\ \end{bmatrix} = 2 \cdot 8 + 7 \cdot 2 + 1 \cdot 8 = 16 + 14+8= 38
$$
于是, 在这里, 引出了**duality**


OK, 还要讨论**linear transformations** from multiple dimensions to one dimension

$$
\vec{v} =
\begin{bmatrix}
2 \\
7
\end{bmatrix}_\text{2d input}
\quad \xrightarrow{\quad L(\vec{v}) \quad} \quad

\begin{bmatrix}
1.8
\end{bmatrix}_\text{1d input}
$$
在这里, 我们的 $\begin{bmatrix}2 \\7\end{bmatrix}$ 从二维变成了一个数(which is 一维的), 
就是  $[1 \quad  3]$ 这种样子, 可以认为是在一维上的两个值, 从原点出发, 指到了1和指到了3, 这样. 
<svg viewBox="0 0 500 120" xmlns="http://www.w3.org/2000/svg">
<!-- Number line -->
<line x1="50" y1="60" x2="450" y2="60" stroke="black" stroke-width="2"/>

<!-- Ticks and labels -->
<g>
<!-- Origin (0) -->
<line x1="250" y1="55" x2="250" y2="65" stroke="black" stroke-width="2"/>
<text x="250" y="80" text-anchor="middle" font-family="Arial" font-size="14">0</text>

<!-- Negative numbers -->
<line x1="210" y1="55" x2="210" y2="65" stroke="black" stroke-width="1"/>
<text x="210" y="80" text-anchor="middle" font-family="Arial" font-size="14">-1</text>

<line x1="170" y1="55" x2="170" y2="65" stroke="black" stroke-width="1"/>
<text x="170" y="80" text-anchor="middle" font-family="Arial" font-size="14">-2</text>

<line x1="130" y1="55" x2="130" y2="65" stroke="black" stroke-width="1"/>
<text x="130" y="80" text-anchor="middle" font-family="Arial" font-size="14">-3</text>

<line x1="90" y1="55" x2="90" y2="65" stroke="black" stroke-width="1"/>
<text x="90" y="80" text-anchor="middle" font-family="Arial" font-size="14">-4</text>

<line x1="50" y1="55" x2="50" y2="65" stroke="black" stroke-width="1"/>
<text x="50" y="80" text-anchor="middle" font-family="Arial" font-size="14">-5</text>

<!-- Positive numbers -->
<line x1="290" y1="55" x2="290" y2="65" stroke="black" stroke-width="1"/>
<text x="290" y="80" text-anchor="middle" font-family="Arial" font-size="14">1</text>

<line x1="330" y1="55" x2="330" y2="65" stroke="black" stroke-width="1"/>
<text x="330" y="80" text-anchor="middle" font-family="Arial" font-size="14">2</text>

<line x1="370" y1="55" x2="370" y2="65" stroke="black" stroke-width="1"/>
<text x="370" y="80" text-anchor="middle" font-family="Arial" font-size="14">3</text>

<line x1="410" y1="55" x2="410" y2="65" stroke="black" stroke-width="1"/>
<text x="410" y="80" text-anchor="middle" font-family="Arial" font-size="14">4</text>

<line x1="450" y1="55" x2="450" y2="65" stroke="black" stroke-width="1"/>
<text x="450" y="80" text-anchor="middle" font-family="Arial" font-size="14">5</text>
</g>

<!-- Vector 1 (blue, pointing to 1) -->
<line x1="250" y1="60" x2="290" y2="60" stroke="blue" stroke-width="3"/>
<polygon points="290,60 285,55 285,65" fill="blue"/>
<text x="275" y="45" font-family="Arial" font-size="14" fill="blue">v₁</text>

<!-- Vector 2 (red, pointing to 3) -->
<line x1="250" y1="60" x2="370" y2="60" stroke="red" stroke-width="3"/>
<polygon points="370,60 365,55 365,65" fill="red"/>
<text x="320" y="45" font-family="Arial" font-size="14" fill="red">v₂</text>
</svg>
所以, 我们几乎可以认为, 1和3是纯数值, 然后这个躺下来的 vector其实 T 一下, 就是一个正常的vector, 这个非常common的操作, 其实建立起了数值 和 vector(2维/3维下的坐标点)之间的关系, 





就是说, 如果我们忘记对于 dot product 公式机械的记忆, 从几何意义开始探讨的话, 那个$[x_1 \quad  x_2 \dots x_n]$ (个数未定义) 的横向的object, 可以被认为是一个 $f(x)$ 把我们可观察的vector们(当然也包括不可观察的), 从2维3维空间, 拉到一个一维的穿过原点的坐标轴上(这里  $x_1\dots x_n$在上面, 就是实际值),这个过程or变化是线性的, 注意这个 $f(x)$ 的output是 1个值. 


一开始对10:04对称的那个截图, 有疑惑, 为什么这里  $\vec{u}$ 我们就默认是1, 哦, 这里又是这个数轴上的单位向量, 然后,  x横线的  $[x_1 \quad x_2 ]$ 其实是什么呢, 是我们的2D的坐标系下的单位向量  $\vec{i} , \vec{j}$ , 投影到那个数轴上时候, 得到的数值, 
<svg viewBox="0 0 500 400" xmlns="http://www.w3.org/2000/svg">
<defs>
<!-- 更小的蓝色箭头 -->
<marker id="blueArrow" markerWidth="4" markerHeight="2.8"
refX="4" refY="1.4" orient="auto" markerUnits="strokeWidth">
<polygon points="0 0, 4 1.4, 0 2.8" fill="blue"/>
</marker>

<!-- 更小的红色箭头 -->
<marker id="redArrow" markerWidth="4" markerHeight="2.8"
refX="4" refY="1.4" orient="auto" markerUnits="strokeWidth">
<polygon points="0 0, 4 1.4, 0 2.8" fill="red"/>
</marker>

<!-- 黑色数轴箭头保持不变 -->
<marker id="axisArrow" markerWidth="6" markerHeight="4.2"
refX="6" refY="2.1" orient="auto" markerUnits="strokeWidth">
<polygon points="0 0, 6 2.1, 0 4.2" fill="black"/>
</marker>
</defs>

<!-- 坐标轴背景 -->
<line x1="50" y1="200" x2="450" y2="200" stroke="#888" stroke-width="1.5" stroke-dasharray="5,5"/>
<polygon points="450,200 440,195 440,205" fill="#888"/>
<text x="460" y="205" font-family="Arial" font-size="14" fill="#888">x</text>

<line x1="250" y1="350" x2="250" y2="50" stroke="#888" stroke-width="1.5" stroke-dasharray="5,5"/>
<polygon points="250,50 245,60 255,60" fill="#888"/>
<text x="255" y="50" font-family="Arial" font-size="14" fill="#888">y</text>

<circle cx="250" cy="200" r="4" fill="#888"/>
<text x="235" y="220" font-family="Arial" font-size="14" fill="#888">O</text>

<!-- 斜向数轴 -->
<line x1="100" y1="300" x2="400" y2="100"
stroke="black" stroke-width="2" marker-end="url(#axisArrow)"/>

<!-- 数轴刻度 -->
<g font-family="Arial" font-size="12" fill="black">
<circle cx="150" cy="266" r="2"/><text x="140" y="260">-5</text>
<circle cx="170" cy="253" r="2"/><text x="160" y="247">-4</text>
<circle cx="190" cy="240" r="2"/><text x="180" y="234">-3</text>
<circle cx="210" cy="227" r="2"/><text x="200" y="221">-2</text>
<circle cx="230" cy="214" r="2"/><text x="220" y="208">-1</text>
<circle cx="250" cy="200" r="2"/><text x="240" y="194">0</text>
<circle cx="270" cy="186" r="2"/><text x="270" y="176">1</text>
<circle cx="290" cy="172" r="2"/><text x="290" y="162">2</text>
<circle cx="310" cy="158" r="2"/><text x="310" y="148">3</text>
<circle cx="330" cy="144" r="2"/><text x="330" y="134">4</text>
<circle cx="350" cy="130" r="2"/><text x="350" y="120">5</text>
</g>

<!-- 红色向量 v₂ -->
<line x1="250" y1="200" x2="310" y2="158"
stroke="red" stroke-width="3" stroke-opacity="0.6"
marker-end="url(#redArrow)"/>
<text x="295" y="150" font-family="Arial" font-size="14" fill="red">v₂</text>

<!-- 蓝色向量 v₁ -->
<line x1="250" y1="200" x2="270" y2="186"
stroke="blue" stroke-width="3"
marker-end="url(#blueArrow)"/>
<text x="255" y="180" font-family="Arial" font-size="14" fill="blue">v₁</text>
</svg>



OK, 这里我们记住了这个特性之后, 会发现对于 2D的空间来说, $[x_1 \quad x_2 ]$ 是我们的单位向量  $\vec{i} , \vec{j}$ 在那个数轴上的投影, 那么现在, 我们比如有一个正常的arbitrary的matrix后, 比如 $\begin{bmatrix}2 \\7\end{bmatrix}$ 我们当然发现2和7就是对于x_1和x_2的, 而没有之前的vector地位不等价的疑惑了, 因为从分开的角度来说, 我们的2确实就和 $\vec{i}$ 有关系, 我们的7确实就和 $\vec{j}$ 有关系, 这是最后发生在一个数轴上的


在之前 乘 3, 其实对于  $\vec{i},\vec{j}$ 来说, 我们对于每一行都乘了3, which 回到之前的问题, $2\times \vec{v} \cdot \vec{w}$这个地方, 我们其实是$\begin{bmatrix}2 \cdot v_{row1} \\ 2 \cdot v_{row2}\end{bmatrix}$ 所以, 这里二维的单位向量都乘了3, 


这个横向的vector又是怎么竖过来的呢?

## Claude 回答

点积的本质可以从两个角度理解：几何投影和线性变换。
从几何角度看，当我们计算 $\vec{v} \cdot \vec{w}$ 时，可以理解为 $\vec{w}$ 在 $\vec{v}$ 方向上的投影长度乘以 $\vec{v}$ 的长度。这就是为什么当我们把 $\vec{v}$ 放大两倍变成 $2\vec{v}$ 时，点积值会变成原来的两倍 - 因为参考向量的长度变了。

从线性变换的角度看，横向的向量 $[a \quad b]$ 定义了一个从二维到一维的映射规则：把空间中的任何向量 $\begin{bmatrix} v_1 \ v_2 \end{bmatrix}$ 映射到数轴上的 $av_1 + bv_2$ 这个点。这不是描述空间中的一个位置，而是描述如何将其他向量映射到一维空间。

当我们计算点积 $[a \quad b] \cdot \begin{bmatrix} v_1 \ v_2 \end{bmatrix} = av_1 + bv_2$ 时，实际上是在应用这个线性变换。当我们把 $[a \quad b]$ 变成 $[2a \quad 2b]$ 时，我们改变了映射规则，所以结果自然变为原来的两倍。

这种视角消除了点积中向量角色不对称的困惑 - 它们本来就是不同的：一个是变换规则，另一个是被变换的对象。这就是线性代数中"对偶性"的本质 - 同一个数学对象可以有两种不同但等价的解释。




我们得出来, 下面的想法, 不是把向量当作空间中一支“箭头”, 而是把它理解为“某种线性变换的具象表现” ,它代表的是一个**作用规则**，不是一个位置或方向

到12:37学不动了, 又回到了duality


## 2025-05-02 新的一天, 图书馆继续

首先是回顾, 我在refine完上面的文章之后, 我感觉又回到了之前的问题, 在这个文章中, 哪些内容, 还不够有intuition, 我感觉从二维到1维的时候, 还是有点困惑是, 为什么  $[x_1 \quad x_2 ] \cdot \begin{bmatrix} x_m \\ x_n \end{bmatrix}$ 为什么这里 $x_m$ 只需要和  $x_1$ 乘,  $x_n$ 只需要和  $x_2$ 乘, 这里还是有点疑惑
## Claude say

从二维到一维的映射
首先，让我们回顾一下点积的核心问题：为什么在 $[x_1 \quad x_2] \cdot \begin{bmatrix} x_m \\ x_n \end{bmatrix}$ 中，$x_1$ 只与 $x_m$ 相乘，$x_2$ 只与 $x_n$ 相乘？
这个问题涉及到向量的对偶性理解。从传统视角看，点积似乎是一个神奇的规则，但从线性变换的角度来看，这个规则非常自然。

## 从线性变换的角度理解点积

当我们把行向量 $[x_1 \quad x_2]$ 看作是一个**线性变换**时，它定义了一种从二维空间到一维数轴的映射规则：

$f([a, b]) = x_1 \cdot a + x_2 \cdot b$

这个函数 $f$ 将二维空间中的任何向量映射到数轴上的一个点。这里的直觉是：

1. 行向量 $[x_1 \quad x_2]$ 不再是空间中的"箭头"，而是一个**变换规则**
2. 这个规则告诉我们如何将二维空间压缩到一维空间
3. $x_1$ 和 $x_2$ 分别是基向量 $\hat{i}$ 和 $\hat{j}$ 在这个映射下的"影像"
<font color='red'>OK,上面这个概念出现不懂, or 有问题, 跳</font> 
当我们计算 $[x_1 \quad x_2] \cdot [x_m \\\ x_n]$ 时，我们实际上是在应用这个变换规则到向量 $[x_m, x_n]$ 上： $f([x_m, x_n]) = x_1 \cdot x_m + x_2 \cdot x_n$

## 对于 3. $x_1$ 和 $x_2$ 分别是基向量 $\hat{i}$ 和 $\hat{j}$ 在这个映射下的"影像", 不懂, 再想

点积的本质理解
点积 $[x_1 \quad x_2] \times \begin{bmatrix} x_m \\ x_n \end{bmatrix} = x_1x_m + x_2x_n$ 之所以是这样计算，本质上是因为这是标准内积的定义方式。
但为什么是这样定义的呢？

**1.从坐标分解的角度**

标准基向量 $\hat{i}$ 和 $\hat{j}$ 是相互正交的。当我们将向量 $\vec{v} = \begin{bmatrix} x_m \\ x_n \end{bmatrix}$ 表示为 $x_m\hat{i} + x_n\hat{j}$ 时，$x_m$ 和 $x_n$ 实际上是向量在这两个基方向上的投影长度。

同样，向量 $\vec{u} = [x_1 \quad x_2]$ 也可以视为 $x_1\hat{i} + x_2\hat{j}$。

当我们计算 $\vec{u} \cdot \vec{v}$ 时，我们在计算： $(x_1\hat{i} + x_2\hat{j}) \cdot (x_m\hat{i} + x_n\hat{j})$

展开后得到： $x_1x_m(\hat{i} \cdot \hat{i}) + x_1x_n(\hat{i} \cdot \hat{j}) + x_2x_m(\hat{j} \cdot \hat{i}) + x_2x_n(\hat{j} \cdot \hat{j})$

由于 $\hat{i} \cdot \hat{i} = 1$，$\hat{j} \cdot \hat{j} = 1$，而 $\hat{i} \cdot \hat{j} = 0$（正交性），所以结果简化为： $x_1x_m + x_2x_n$

这就是为什么我们只需要将对应分量相乘并求和 - 正交基消除了交叉项！

### 2. 从线性变换的角度

当我们将 $[x_1 \quad x_2]$ 视为线性变换时，它完全由对基向量的作用确定：

- 将 $\hat{i}$ 映射到 $x_1$
- 将 $\hat{j}$ 映射到 $x_2$

对任意向量 $\begin{bmatrix} x_m \ x_n \end{bmatrix} = x_m\hat{i} + x_n\hat{j}$ 的作用是： $x_m$ 的部分贡献 $x_m \cdot x_1$ $x_n$ 的部分贡献 $x_n \cdot x_2$

总和是 $x_1x_m + x_2x_n$

我感觉这里LLM模型的解释是shit, 我觉得从svg的地方再开始自己理清楚一下应该可以清楚.
我们得到了一个数轴上的1和3, 和 $[1 \quad 3]$ 然后这个数轴是在二维坐标系上的, 我重复一遍这个svg如下, 那么, 其实在这个数轴上, 等于1和等于3的vector本身, 就是使用二维平面上的标准基向量 $\hat{i}$ 和 $\hat{j}$ 构建的, 
<svg viewBox="0 0 500 400" xmlns="http://www.w3.org/2000/svg">
<defs>
<!-- 更小的蓝色箭头 -->
<marker id="blueArrow" markerWidth="4" markerHeight="2.8"
refX="4" refY="1.4" orient="auto" markerUnits="strokeWidth">
<polygon points="0 0, 4 1.4, 0 2.8" fill="blue"/>
</marker>

<!-- 更小的红色箭头 -->
<marker id="redArrow" markerWidth="4" markerHeight="2.8"
refX="4" refY="1.4" orient="auto" markerUnits="strokeWidth">
<polygon points="0 0, 4 1.4, 0 2.8" fill="red"/>
</marker>

<!-- 黑色数轴箭头保持不变 -->
<marker id="axisArrow" markerWidth="6" markerHeight="4.2"
refX="6" refY="2.1" orient="auto" markerUnits="strokeWidth">
<polygon points="0 0, 6 2.1, 0 4.2" fill="black"/>
</marker>
</defs>

<!-- 坐标轴背景 -->
<line x1="50" y1="200" x2="450" y2="200" stroke="#888" stroke-width="1.5" stroke-dasharray="5,5"/>
<polygon points="450,200 440,195 440,205" fill="#888"/>
<text x="460" y="205" font-family="Arial" font-size="14" fill="#888">x</text>

<line x1="250" y1="350" x2="250" y2="50" stroke="#888" stroke-width="1.5" stroke-dasharray="5,5"/>
<polygon points="250,50 245,60 255,60" fill="#888"/>
<text x="255" y="50" font-family="Arial" font-size="14" fill="#888">y</text>

<circle cx="250" cy="200" r="4" fill="#888"/>
<text x="235" y="220" font-family="Arial" font-size="14" fill="#888">O</text>

<!-- 斜向数轴 -->
<line x1="100" y1="300" x2="400" y2="100"
stroke="black" stroke-width="2" marker-end="url(#axisArrow)"/>

<!-- 数轴刻度 -->
<g font-family="Arial" font-size="12" fill="black">
<circle cx="150" cy="266" r="2"/><text x="140" y="260">-5</text>
<circle cx="170" cy="253" r="2"/><text x="160" y="247">-4</text>
<circle cx="190" cy="240" r="2"/><text x="180" y="234">-3</text>
<circle cx="210" cy="227" r="2"/><text x="200" y="221">-2</text>
<circle cx="230" cy="214" r="2"/><text x="220" y="208">-1</text>
<circle cx="250" cy="200" r="2"/><text x="240" y="194">0</text>
<circle cx="270" cy="186" r="2"/><text x="270" y="176">1</text>
<circle cx="290" cy="172" r="2"/><text x="290" y="162">2</text>
<circle cx="310" cy="158" r="2"/><text x="310" y="148">3</text>
<circle cx="330" cy="144" r="2"/><text x="330" y="134">4</text>
<circle cx="350" cy="130" r="2"/><text x="350" y="120">5</text>
</g>

<!-- 红色向量 v₂ -->
<line x1="250" y1="200" x2="310" y2="158"
stroke="red" stroke-width="3" stroke-opacity="0.6"
marker-end="url(#redArrow)"/>
<text x="295" y="150" font-family="Arial" font-size="14" fill="red">v₂</text>

<!-- 蓝色向量 v₁ -->
<line x1="250" y1="200" x2="270" y2="186"
stroke="blue" stroke-width="3"
marker-end="url(#blueArrow)"/>
<text x="255" y="180" font-family="Arial" font-size="14" fill="blue">v₁</text>
</svg>

OK, 再回过来注意什么, 我们的 标准基向量 $\hat{i}$ 和 $\hat{j}$ 在所谓的第一次变换后, 变成了1, 在第二次变换后变成了3(我觉得这里还是可以按照一列一列来理解, 只不过这里一列就一个数字, 有两列), 那么是怎么在这个位置上的, OK, 这是我之前没解决的点, 我重新看了视频, 虽然, 在这个位置上, 我的意思是, 虽然  $v_1$  $v_2$ 在那个位置上好像要用到标准基向量 $\hat{i}$ 和 $\hat{j}$ 来固定, 但是想想是怎么固定的, 就是应该被怎么算出来在那个位置, 好像怎么都想不到只有一行的raw的 $[1 \quad 3]$ 

**视频5:46到6:04**, 这里说想象一个线性变换, 然后直接把j拉到一个一维的数轴上-2位置, i还保持原来的位置(1,0), 只不过刚好是数轴的1, 这里的i的0其实没有体现出来
- 基向量 $\hat{i} = \begin{bmatrix} 1 \ 0 \end{bmatrix}$ 被映射到数轴上的位置1
- 基向量 $\hat{j} = \begin{bmatrix} 0 \ 1 \end{bmatrix}$ 被映射到数轴上的位置-2
这是因为这个变换将二维空间压缩成了一维空间，所以必然会丢失一些信息。
这个线性变换可以用行向量 $[1 \quad -2]$ 来表示，意味着：

- 任何向量 $\begin{bmatrix} a \\ b \end{bmatrix}$ 会被映射到数轴上的 $1 \cdot a + (-2) \cdot b = a - 2b$
问题... 如果按照 列空间的想法的话, 这里 $[1 \quad-2] \times \begin{bmatrix} a \\ b \end{bmatrix}$ 然后,  $a * [1] + a*[-2]$ , 哦这里混淆了, 不可以这样写, 这个矩阵乘法是不可以成立的, 点乘和矩阵乘法理论上是两种东西?

<svg viewBox="0 0 700 225" xmlns="http://www.w3.org/2000/svg">
  <!-- 背景 -->
  <rect width="100%" height="100%" fill="black"/>

  <!-- Transform 标签 -->
  <text x="60" y="40" font-size="28" fill="skyblue" font-family="Courier New">Transform</text>

  <!-- Transform 行向量 -->
  <text x="50" y="100" font-size="36" fill="white" font-family="Courier New">[</text>
  <text x="80" y="100" font-size="36" fill="lightgreen" font-family="Courier New">1</text>
  <text x="120" y="100" font-size="36" fill="salmon" font-family="Courier New">-2</text>
  <text x="160" y="100" font-size="36" fill="white" font-family="Courier New">]</text>

  <!-- Vector 列向量大括号实现 -->
  <!-- 左中括号 -->
  <line x1="210" y1="59" x2="210" y2="161" stroke="white" stroke-width="2"/> <!-- 长竖线 -->
  <line x1="210" y1="60" x2="220" y2="60" stroke="white" stroke-width="2"/>
  <line x1="210" y1="160" x2="220" y2="160" stroke="white" stroke-width="2"/>

  <!-- 右中括号 -->
  <line x1="260" y1="59" x2="260" y2="161" stroke="white" stroke-width="2"/>
  <line x1="250" y1="60" x2="260" y2="60" stroke="white" stroke-width="2"/>
  <line x1="250" y1="160" x2="260" y2="160" stroke="white" stroke-width="2"/>

  <!-- 列向量内容，使用等宽字体 -->
  <text x="235" y="95" font-size="36" fill="lightgreen" font-family="Courier New" text-anchor="middle">4</text>
  <text x="235" y="145" font-size="36" fill="salmon" font-family="Courier New" text-anchor="middle">3</text>

  <!-- Vector 标签 -->
  <text x="215" y="190" font-size="28" fill="gold" font-family="Courier New">Vector</text>

  <!-- 等号 -->
  <text x="300" y="110" font-size="36" fill="white" font-family="Courier New">=</text>

  <!-- 点积展开式 -->
  <text x="350" y="110" font-size="36" font-family="Courier New">
    <tspan fill="lightgreen">4</tspan>
    <tspan fill="white">·</tspan>
    <tspan fill="lightgreen">1</tspan>
    <tspan fill="white"> + </tspan>
    <tspan fill="salmon">3</tspan>
    <tspan fill="white">·</tspan>
    <tspan fill="salmon">-2</tspan>
  </text>
</svg>


寄了, 我感觉我没法在逻辑上理解为什么这个转秩一下是一样的


虽然过程混乱, 但是问题被总结为, 为什么对于$\begin{bmatrix} 3 \ 4 \end{bmatrix} \times \begin{bmatrix} 5 \\ 2 \end{bmatrix}$和 $\begin{bmatrix} 3 \\ 4 \end{bmatrix} \cdot \begin{bmatrix} 5 \\ 2 \end{bmatrix}$ 是不是地位等价?  为什么3 只可以和5乘呢? 这个从2维到1维的变换中,  $\begin{bmatrix} 3 \ 4 \end{bmatrix}$ 只被认为是变换器的角色


视频的8:45

<svg viewBox="0 0 700 300" xmlns="http://www.w3.org/2000/svg">
  <!-- 黑色背景 -->
  <rect width="100%" height="100%" fill="black"/>

  <!-- 标题 -->
  <text x="50" y="155" font-size="28" fill="white" font-family="Courier New">Projection matrix:</text>

  <!-- 左中括号 -->
  <line x1="380" y1="130" x2="380" y2="170" stroke="white" stroke-width="2"/>
  <line x1="380" y1="130" x2="390" y2="130" stroke="white" stroke-width="2"/>
  <line x1="380" y1="170" x2="390" y2="170" stroke="white" stroke-width="2"/>

  <!-- 右中括号 -->
  <line x1="490" y1="130" x2="490" y2="170" stroke="white" stroke-width="2"/>
  <line x1="480" y1="130" x2="490" y2="130" stroke="white" stroke-width="2"/>
  <line x1="480" y1="170" x2="490" y2="170" stroke="white" stroke-width="2"/>

  <!-- 矩阵元素问号 -->
  <text x="400" y="160" font-size="36" fill="lightgreen" font-family="Courier New">?</text>
  <text x="450" y="160" font-size="36" fill="salmon" font-family="Courier New">?</text>

  <!-- 上箭头（î） -->
  <line x1="410" y1="80" x2="410" y2="120" stroke="lightgreen" stroke-width="3" marker-end="url(#arrowGreen)"/>
  <text x="410" y="75" font-size="18" fill="lightgreen" font-family="Courier New">Where î lands</text>

  <!-- 下箭头（ĵ） -->
  <line x1="460" y1="210" x2="460" y2="175" stroke="salmon" stroke-width="3" marker-end="url(#arrowRed)"/>
  <text x="460" y="235" font-size="18" fill="salmon" font-family="Courier New">Where ĵ lands</text>

  <!-- 箭头定义 -->
  <defs>
    <marker id="arrowGreen" markerWidth="6" markerHeight="6" refX="3" refY="3" orient="auto">
      <polygon points="0,0 6,3 0,6" fill="lightgreen"/>
    </marker>
    <marker id="arrowRed" markerWidth="6" markerHeight="6" refX="3" refY="3" orient="auto">
      <polygon points="0,0 6,3 0,6" fill="salmon"/>
    </marker>
  </defs>
</svg>



为什么要这样, 就是在这个穿过原点的数轴被建立之后, 这里的 $[x_1,x_2]$ 其实就是下面的 $\hat{u}$ 的作为在二维坐标轴上的值, 但是注意同时也是标准基向量 $\hat{i}$ 和 $\hat{j}$ 到那个一维数轴上的投影长度, 




<svg width="600" height="300" viewBox="-150 -170 300 300" xmlns="http://www.w3.org/2000/svg" style="background-color: black;">

  <defs>
    <marker id="arrowhead_yellow" markerWidth="7" markerHeight="5" refX="6" refY="2.5" orient="auto" markerUnits="strokeWidth">
      <polygon points="0 0, 7 2.5, 0 5" fill="yellow"/>
    </marker>
    <marker id="arrowhead_dk_yellow" markerWidth="7" markerHeight="5" refX="6" refY="2.5" orient="auto" markerUnits="strokeWidth">
      <polygon points="0 0, 7 2.5, 0 5" fill="lightgreen"/>
    </marker>
    <marker id="arrowhead_salmon" markerWidth="7" markerHeight="5" refX="6" refY="2.5" orient="auto" markerUnits="strokeWidth">
      <polygon points="0 0, 7 2.5, 0 5" fill="salmon"/>
    </marker>
    <symbol id="tick" viewBox="-1 -5 2 10">
        <line x1="0" y1="-4" x2="0" y2="4" stroke-width="1"/>
    </symbol>
  </defs>

  <g id="grid" stroke="#add8e6" stroke-width="0.5">
     <line x1="-300" y1="-300" x2="-300" y2="300"/> <line x1="-200" y1="-300" x2="-200" y2="300"/> <line x1="-100" y1="-300" x2="-100" y2="300"/> <line x1="0"    y1="-300" x2="0"    y2="300" stroke-width="1"/> <line x1="100"  y1="-300" x2="100"  y2="300"/> <line x1="200"  y1="-300" x2="200"  y2="300"/> <line x1="300"  y1="-300" x2="300"  y2="300"/> <line x1="-300" y1="-300" x2="300" y2="-300"/> <line x1="-300" y1="-200" x2="300" y2="-200"/> <line x1="-300" y1="-100" x2="300" y2="-100"/> <line x1="-300" y1="0"    x2="300" y2="0" stroke-width="1"/> <line x1="-300" y1="100"  x2="300" y2="100"/> <line x1="-300" y1="200"  x2="300" y2="200"/> <line x1="-300" y1="300"  x2="300" y2="300"/> </g>

  <g id="lines">
    <line x1="-300" y1="124.2" x2="300" y2="-124.2" stroke="white" stroke-width="2.2" stroke-dasharray="5, 5"/>
    <text x="-210" y="130" fill="white" font-family="Courier New" font-size="16" transform="rotate(-22.5 -280 130)" text-anchor="start">Line of symmetry</text>

    <line x1="-300" y1="300" x2="300" y2="-300" stroke="lightblue" stroke-width="2.2"/>
  </g>

  <g id="blue_axis_markings" fill="grey" font-family="Courier New" font-size="20" text-anchor="middle">
         <g transform="translate(282.8, -282.8)"> <use href="#tick" stroke="white" />
             <text dx="10" dy="-10" >2</text>
        </g>
        <g transform="translate(-141.4, 141.4)"> <use href="#tick" stroke="white" transform="rotate(-45) rotate(90)" />
             <text dx="-10" dy="10" >-1</text>
        </g>
        <g transform="translate(-282.8, 282.8)"> <use href="#tick" stroke="white" />
             <text dx="-10" dy="10" >-2</text>
        </g>
   </g>

  <g id="vectors_projections">
     <line x1="0" y1="0" x2="200" y2="0" stroke="lightgreen" stroke-width="2" marker-end="url(#arrowhead_dk_yellow)"/>
    <text x="205" y="-5" fill="lightgreen" font-family="serif" font-style="italic" font-size="28" >î</text>

    <line x1="0" y1="0" x2="140" y2="-140" stroke="yellow" stroke-width="2" marker-end="url(#arrowhead_yellow)"/>
    <text x="146" y="-146" fill="yellow" font-family="serif" font-style="italic" font-size="28" >û</text>

    <line x1="141.4" y1="-141.4" x2="141.4" y2="0" stroke="grey" stroke-width="1" stroke-dasharray="3, 3"/>

    <line x1="200" y1="0" x2="100" y2="-100" stroke="grey" stroke-width="1" stroke-dasharray="3, 3"/>

    <line x1="0" y1="0" x2="100" y2="-100"
          stroke="salmon" stroke-width="2" stroke-dasharray="4,4"
          opacity="1.0" marker-end="url(#arrowhead_salmon)"/>
    <text x="105" y="-85" fill="salmon" font-family="sans-serif" font-style="italic" font-size="16">u<tspan baseline-shift="sub" font-size="12">x</tspan></text>

    <line x1="0" y1="0" x2="141.4" y2="0"
          stroke="salmon" stroke-width="2" stroke-dasharray="4,4"
          opacity="1.0" marker-end="url(#arrowhead_salmon)"/>
     <text x="120.7" y="-15" fill="salmon" font-family="sans-serif" font-style="italic" font-size="16" text-anchor="middle">u<tspan baseline-shift="sub" font-size="12">x</tspan></text>

  </g>

  <g id="text_labels" fill="white" font-family="sans-serif">
    <text x="-290" y="-280" font-size="16">Where do <tspan font-family="serif" font-style="italic">î</tspan> and <tspan font-family="serif" font-style="italic">ĵ</tspan> land?</text>
    <text x="-270" y="-260" font-size="16" font-family="monospace">[ </text>
    <text x="-220" y="-260" font-size="16" font-family="monospace">]</text>
    <text x="5" y="15" font-size="20">o</text> <text x="200" y="20" font-size="20" text-anchor="middle">1</text>
    <text x="-200" y="20" font-size="20" text-anchor="middle">-1</text>
    <text x="-5" y="-193" font-size="20" text-anchor="end">1</text>
    <text x="-5" y="207" font-size="20" text-anchor="end">-1</text>
  </g>

</svg>








![[Screenshot 2025-05-02 at 11.10.30 PM.png]]

OK, 那问题好像解决了, 就对于二维 $\begin{bmatrix} a \\ b \end{bmatrix}$ 来说, 它中作为一个点or一个箭头, 我们的 $a$ 和 $b$ 各是标准基向量 $\hat{i}$ 和 $\hat{j}$ 构建的, 如果要 onto 到我们的数轴上, 当然, 只能 grab 我们对应的数值

<svg viewBox="0 0 650 280" xmlns="http://www.w3.org/2000/svg">
  <!-- 背景 -->
  <rect width="100%" height="100%" fill="black"/>

  <!-- “Transform” 标签 -->
  <text x="55" y="90" font-size="28" fill="skyblue" font-family="Courier New">Transform</text>

  <!-- 行向量 [uₓ uᵧ] -->
  <text x="60" y="132" font-size="36" fill="white" font-family="Courier New">[</text>
  <text x="90" y="130" font-size="36" font-family="Courier New">
    <tspan fill="#CCCC66">u</tspan>
    <!-- 下标微调 -->
    <tspan dx="-20px" dy="2px" baseline-shift="-10%" font-size="24" fill="#88CC88">x</tspan>
  </text>
  <text x="150" y="130" font-size="36" font-family="Courier New">
    <tspan fill="#CCCC66">u</tspan>
    <tspan dx="-20px" dy="2px" baseline-shift="-10%" font-size="24" fill="#E59494">y</tspan>
  </text>
  <text x="190" y="132" font-size="36" fill="white" font-family="Courier New">]</text>

  <!-- 列向量 [x; y] 用中括号和线条 -->
  <!-- 左中括号 -->
  <line x1="230" y1="80" x2="230" y2="180" stroke="white" stroke-width="2"/>
  <line x1="230" y1="80" x2="240" y2="80" stroke="white" stroke-width="2"/>
  <line x1="230" y1="180" x2="240" y2="180" stroke="white" stroke-width="2"/>
  <!-- 右中括号 -->
  <line x1="290" y1="80" x2="290" y2="180" stroke="white" stroke-width="2"/>
  <line x1="280" y1="80" x2="290" y2="80" stroke="white" stroke-width="2"/>
  <line x1="280" y1="180" x2="290" y2="180" stroke="white" stroke-width="2"/>
  <!-- 列向量内容 -->
  <text x="260" y="110" font-size="36" fill="#CC88CC" font-family="Courier New" text-anchor="middle">x</text>
  <text x="260" y="160" font-size="36" fill="#CC88CC" font-family="Courier New" text-anchor="middle">y</text>

  <!-- “Vector” 标签 -->
  <text x="210" y="220" font-size="28" fill="#CC88CC" font-family="Courier New">Vector</text>

  <!-- 等号 -->
  <text x="310" y="135" font-size="36" fill="#EEEEEE" font-family="Courier New">=</text>

  <!-- 点积展开式 uₓ·x + uᵧ·y，紧凑且饱和度降低 -->
  <text x="340" y="135" font-size="36" font-family="Courier New">
    <tspan>
      <tspan fill="#CCCC66">u</tspan>
      <tspan dx="-20px" dy="2px" baseline-shift="-10%" font-size="24" fill="#88CC88">x</tspan>
    </tspan>
    <tspan fill="#EEEEEE" dx="-30px">·</tspan>
    <tspan fill="#CC88CC" dx="-12px">x</tspan>
    <tspan fill="#EEEEEE" dx="-4px"> + </tspan>
    <tspan>
      <tspan fill="#CCCC66">u</tspan>
      <tspan dx="-20px" dy="2px" baseline-shift="-10%" font-size="24" fill="#E59494">y</tspan>
    </tspan>
    <tspan fill="#EEEEEE" dx="-25px">·</tspan>
    <tspan fill="#CC88CC" dx="-12px">y</tspan>
  </text>
</svg>

first projecting onto that vector

这里建立了数值和vector的联系, 就是说, 我们横向的一维度的object(指这里的 $u_x \dots to\dots u_y$), 可以认为是一个个变换运动(跳出2维), 但是同时, 这里把这个动作(们)对称回去, 也可以是我们的向量(也就是竖着的), 
这里从直觉上不对称的投影行为, 被我们整理成一个个可以理解的变换了, 然后注意, 对称也实现了如何实现的, 在倒数第二个截图的位置, 在$\hat{i}$ 在  $\hat{u}$ 所在的数轴上是一个数值(这描述一个变换), 同时 $\hat{u}$在 $\hat{i}$ 的方向上, 如果被表示成一个数, 是$\hat{u}$ 向量在二维坐标系中, $\hat{i}$方向上的分量. 
这里的数值是一样的, 这里的变换是对称的, 只是我们从图像上给他们赋予的实际意义不同, 太美了,这是duality. 





# Appendix

一张被淘汰的作图

<svg width="600" height="600" viewBox="-300 -300 600 600" xmlns="http://www.w3.org/2000/svg" style="background-color: black;">

  <defs>
    <marker id="arrowhead_yellow" markerWidth="7" markerHeight="5" refX="6" refY="2.5" orient="auto" markerUnits="strokeWidth">
      <polygon points="0 0, 7 2.5, 0 5" fill="yellow"/>
    </marker>
    <marker id="arrowhead_dk_yellow" markerWidth="7" markerHeight="5" refX="6" refY="2.5" orient="auto" markerUnits="strokeWidth">
      <polygon points="0 0, 7 2.5, 0 5" fill="lightgreen"/>
    </marker>
    <marker id="arrowhead_salmon" markerWidth="7" markerHeight="5" refX="6" refY="2.5" orient="auto" markerUnits="strokeWidth">
      <polygon points="0 0, 7 2.5, 0 5" fill="salmon"/>
    </marker>
    <symbol id="tick" viewBox="-1 -5 2 10">
        <line x1="0" y1="-4" x2="0" y2="4" stroke-width="1"/>
    </symbol>
  </defs>

  <g id="grid" stroke="#add8e6" stroke-width="0.5">
     <line x1="-300" y1="-300" x2="-300" y2="300"/> <line x1="-200" y1="-300" x2="-200" y2="300"/> <line x1="-100" y1="-300" x2="-100" y2="300"/> <line x1="0"    y1="-300" x2="0"    y2="300" stroke-width="1"/> <line x1="100"  y1="-300" x2="100"  y2="300"/> <line x1="200"  y1="-300" x2="200"  y2="300"/> <line x1="300"  y1="-300" x2="300"  y2="300"/> <line x1="-300" y1="-300" x2="300" y2="-300"/> <line x1="-300" y1="-200" x2="300" y2="-200"/> <line x1="-300" y1="-100" x2="300" y2="-100"/> <line x1="-300" y1="0"    x2="300" y2="0" stroke-width="1"/> <line x1="-300" y1="100"  x2="300" y2="100"/> <line x1="-300" y1="200"  x2="300" y2="200"/> <line x1="-300" y1="300"  x2="300" y2="300"/> </g>

  <g id="lines">
    <line x1="-300" y1="124.2" x2="300" y2="-124.2" stroke="white" stroke-width="2.2" stroke-dasharray="5, 5"/>
    <text x="-280" y="130" fill="white" font-family="sans-serif" font-size="14" transform="rotate(-22.5 -280 130)" text-anchor="start">Line of symmetry</text>

    <line x1="-300" y1="300" x2="300" y2="-300" stroke="lightblue" stroke-width="2.2"/>
  </g>

  <g id="blue_axis_markings" fill="grey" font-family="sans-serif" font-size="20" text-anchor="middle">
        <g transform="translate(141.4, -141.4)"> <use href="#tick" stroke="white" />
             <text dx="10" dy="-10" >1</text>
        </g>
         <g transform="translate(282.8, -282.8)"> <use href="#tick" stroke="white" />
             <text dx="10" dy="-10" >2</text>
        </g>
        <g transform="translate(-141.4, 141.4)"> <use href="#tick" stroke="white" transform="rotate(-45) rotate(90)" />
             <text dx="-10" dy="10" >-1</text>
        </g>
        <g transform="translate(-282.8, 282.8)"> <use href="#tick" stroke="white" />
             <text dx="-10" dy="10" >-2</text>
        </g>
   </g>

  <g id="vectors_projections">
     <line x1="0" y1="0" x2="200" y2="0" stroke="lightgreen" stroke-width="2" marker-end="url(#arrowhead_dk_yellow)"/>
    <text x="205" y="-5" fill="lightgreen" font-family="serif" font-style="italic" font-size="28" >î</text>

    <line x1="0" y1="0" x2="140" y2="-140" stroke="yellow" stroke-width="2" marker-end="url(#arrowhead_yellow)"/>
    <text x="146" y="-146" fill="yellow" font-family="serif" font-style="italic" font-size="28" >û</text>

    <line x1="141.4" y1="-141.4" x2="141.4" y2="0" stroke="grey" stroke-width="1" stroke-dasharray="3, 3"/>

    <line x1="200" y1="0" x2="100" y2="-100" stroke="grey" stroke-width="1" stroke-dasharray="3, 3"/>

    <line x1="0" y1="0" x2="100" y2="-100"
          stroke="salmon" stroke-width="2" stroke-dasharray="4,4"
          opacity="1.0" marker-end="url(#arrowhead_salmon)"/>
    <text x="105" y="-85" fill="salmon" font-family="sans-serif" font-style="italic" font-size="16">u<tspan baseline-shift="sub" font-size="12">x</tspan></text>

    <line x1="0" y1="0" x2="141.4" y2="0"
          stroke="salmon" stroke-width="2" stroke-dasharray="4,4"
          opacity="1.0" marker-end="url(#arrowhead_salmon)"/>
     <text x="120.7" y="-15" fill="salmon" font-family="sans-serif" font-style="italic" font-size="16" text-anchor="middle">u<tspan baseline-shift="sub" font-size="12">x</tspan></text>

  </g>

  <g id="text_labels" fill="white" font-family="sans-serif">
    <text x="-290" y="-280" font-size="16">Where do <tspan font-family="serif" font-style="italic">î</tspan> and <tspan font-family="serif" font-style="italic">ĵ</tspan> land?</text>
    <text x="-270" y="-260" font-size="16" font-family="monospace">[ </text>
    <text x="-220" y="-260" font-size="16" font-family="monospace">]</text>
    <text x="5" y="15" font-size="20">o</text> <text x="200" y="20" font-size="20" text-anchor="middle">1</text>
    <text x="-200" y="20" font-size="20" text-anchor="middle">-1</text>
    <text x="-5" y="-193" font-size="20" text-anchor="end">1</text>
    <text x="-5" y="207" font-size="20" text-anchor="end">-1</text>
  </g>

</svg>
