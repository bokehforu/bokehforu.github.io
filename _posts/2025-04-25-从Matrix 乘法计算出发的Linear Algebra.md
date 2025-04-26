---
layout: post
title: "Linear Algebra Starting from Matrix Multiplication"
date: 2025-04-25
---
好像写成一个的线代的内容了, 有很多未完待续的内容

我可以算出矩阵乘法的题目，但当涉及到矩阵乘法的**交换顺序的意义**，或者说矩阵乘法**本身的内在含义**时，我往往无法在第一时间作出直觉反应。

在做矩阵乘法的时候，我依赖的是一种背诵的技巧, 提醒自己这个东西叫 “行列式”, 所以“前一个矩阵的行, 乘以后一个矩阵的列”。但我并不知道这个操作**实际上意味着什么**。 经过自己的反思，我发现，我之所以缺乏这种直觉，是因为我对“矩阵乘法”这一概念没有真正理解。在除了得到一个结果外, 矩阵乘法到底在干什么。这个很基本的数学定义 or 数学概念想要解决现实中的什么问题?

这种基于死记硬背的方式，让我在进一步思考矩阵相关的概念时(如旋转、投影、缩放等操作, 或者是去括号, 转置, 求可逆矩阵的一些变式)，总是感觉模糊和经常出错。因为从最底层开始，我对矩阵的理解就是模糊的，甚至可以说是错的，导致我没法基于它构建准确的思维。



我想解决这个问题。



线性变换的复合 (Composition of Linear Transformations)

### 出现问题的一个comment的场景
下面是一个 $5 \times 5$ 的矩阵相乘的例子, 这是一个很好的例子就是, 
$$\begin{bmatrix} A_{11} & a_{12} & a_{13} & a_{14} & a_{15} \\ A_{21} & a_{22} & a_{23} & a_{24} & a_{25} \\ A_{31} & a_{32} & a_{33} & a_{34} & a_{35} \\ A_{41} & a_{42} & a_{43} & a_{44} & a_{45} \\ A_{51} & a_{52} & a_{53} & a_{54} & a_{55} \\ \end{bmatrix} \times \begin{bmatrix} B_{11} & b_{12} & b_{13} & b_{14} & b_{15} \\ B_{21} & b_{22} & b_{23} & b_{24} & b_{25} \\ B_{31} & b_{32} & b_{33} & b_{34} & b_{35} \\ B_{41} & b_{42} & b_{43} & b_{44} & b_{45} \\ B_{51} & b_{52} & b_{53} & b_{54} & b_{55} \\ \end{bmatrix} = \begin{bmatrix} C_{11} & c_{12} & c_{13} & c_{14} & c_{15} \\ C_{21} & c_{22} & c_{23} & c_{24} & c_{25} \\ C_{31} & c_{32} & c_{33} & c_{34} & c_{35} \\ C_{41} & c_{42} & c_{43} & c_{44} & c_{45} \\ C_{51} & c_{52} & c_{53} & c_{54} & c_{55} \\ \end{bmatrix}$$ 

疑惑的点是, 如果认为任意一个matrix都是列向量的话, 那么其实在这个显而易见的式子中, $A   x = b$ 中, 一个认知是$A$  可以被认为是一个大的系统(如果是 n by m的matrix), $x$作为一个vector(拆分成竖直方向上的单列) (woc这里应该是 1 乘 多少的单列vector我不可以一秒判断出来), 由于疑惑, 我回到传统想法上的记住行列式的乘法的方法, 会发现, 这个结果也是一列的其实, 但是我对于怎么乘是模糊的, OK再想 行乘以列这个口诀, 也就是说, vector的第一个, 乘了A的第一个行, 这是也是第一个b上的结果, 那么这个第一个位置上的结果到底是什么东西呢, 不是最后要写的结果, 而是搞不明白代表什么东西


# {3Blue1Brown} Linear transformations and matrices | Chapter 3, Essence of linear algebra

回到一个简单的问题, 下面是一个在二维平面中的vector,
$$\vec{v} = \begin{bmatrix} -1 \\ 2 \end{bmatrix}$$ 如何看待这个对象呢, 可以认为是, 使用两个单位矩阵构造的, which is  $\hat{j} = \begin{bmatrix} 0\\ 1 \end{bmatrix}$ 和$\hat{i}= \begin{bmatrix} 1\\ 0 \end{bmatrix}$, 这里可以注意到, $\hat{j}$ 在 $y$ 轴上, 而 $\hat{i}$ 在 $x$ 轴上, 那么我们的 $\begin{bmatrix} -1 \\ 2 \end{bmatrix}$ 是如何得到的呢?  使用线性变换(注:要补充)的概念非常简单, 我们可以得到
$$\vec{v} = (-1) \cdot \hat{i} + 2 \cdot \hat{j} = (-1) \cdot \begin{bmatrix} 1\\ 0 \end{bmatrix} + 2 \cdot \begin{bmatrix} 0\\ 1 \end{bmatrix} = \begin{bmatrix} -1 \\ 2 \end{bmatrix}$$ 

OK, 再进一步的视角是, 
$$  $$


我原来以为, $\begin{bmatrix} -1 \\ 2 \end{bmatrix} \cdot \begin{bmatrix} 1 & 0 \\0 &1 \end{bmatrix}$ 是可以得到 $\begin{bmatrix} -1 \\ 2 \end{bmatrix}$ , 但是现在发现我错了(而且这也是非法的矩阵相乘), 应该是$\begin{bmatrix} 1 & 0 \\0 &1 \end{bmatrix} \cdot \begin{bmatrix} -1 \\ 2 \end{bmatrix}$因为和下面的逻辑混淆了, 3Blue1Brown说, 对于(这里我随机写了一个例子) $\begin{bmatrix} -1 & 4 \\ 1 & 2 \end{bmatrix} \cdot \begin{bmatrix} -1 \\ 2 \end{bmatrix}$ 这里其实是让新的基底变成 $\begin{bmatrix} -1 & 4 \\ 1 & 2 \end{bmatrix}$ 而不再是原来的 $\begin{bmatrix} 1 & 0 \\0 &1 \end{bmatrix}$ 我在想是不是原来对于 $\begin{bmatrix} -1 \\ 2 \end{bmatrix}$ 是不是后面都藏着一个 $\begin{bmatrix} 1 & 0 \\0 &1 \end{bmatrix}$ 代表着原来的基底?

哦哦, 不是的, 应该说一个结果的基座向量会写在结果的前面, $I \cdot \vec{v} = \begin{bmatrix} 1 & 0 \\ 0 & 1 \end{bmatrix} \cdot \begin{bmatrix} -1 \\ 2 \end{bmatrix} = \begin{bmatrix} -1 \\ 2 \end{bmatrix}$, 这样反而是恰当的, 合乎逻辑的, 但是在前面乘一个单位矩阵太傻了, 但是可以发现的是, 在前面乘就是提供 一个要变换的指令, 只不过单位矩阵恰好是没有任何变化要求的那个. 而 $\begin{bmatrix} -1 & 4 \\ 1 & 2 \end{bmatrix} \cdot \begin{bmatrix} -1 \\ 2 \end{bmatrix}$ 可以被认为是$\begin{bmatrix} -1 & 4 \\ 1 & 2 \end{bmatrix} \cdot \begin{bmatrix} 1 & 0 \\ 0 & 1 \end{bmatrix} \cdot \begin{bmatrix} -1 \\ 2 \end{bmatrix}$



<font color='red'>这个表述错了</font> $\rightarrow$ 其实在$\begin{bmatrix} -1 \\ 2 \end{bmatrix}$的后面乘是逆变化, 不过这是后话了. <font color='red'>变化可以认为就是在前面乘, 在前面乘就是在做各种线性操作, 比如转回去就是在前面的位置乘一个逆就行了</font>



但是我好像还是没搞懂为什么能变成这样, $(-1) \cdot \begin{bmatrix} -1 \\ 1\end{bmatrix} \cdot + 2 \cdot  \begin{bmatrix} 4 \\ 2\end{bmatrix}$ 
3Blue1Brown的视频中, 是这样写的, $\begin{bmatrix} -1 \\ 2 \end{bmatrix}$  被我们看成了单独放置的点 or 一个向量的箭头指向这个点的位置, 这样的意义也可以这样表示$\vec{v} = -1 \cdot \vec{i}_1 + 2 \cdot \vec{j}_2$,  这个点的表示分, 我突然看到感觉好陌生, 之前好像没有只是顺着写了一下, 自己不知道为什么可以这样写. OK, 如果可以这样写的话, 就相对清晰了, 就是, 直接换了一套基座, 对于这个式子而言, $\begin{bmatrix} -1 & 4 \\ 1 & 2 \end{bmatrix} \cdot \begin{bmatrix} -1 \\ 2 \end{bmatrix}$ 不是吗, 


## 再描述一个更加抽象的例子

$$ A \cdot B = C$$

这里的$A$ 和 $B$ 都是 $4 \times 4$ 的matrix

从列的角度看这个问题后, <font color='red'>好吧, 突然我也不知道这里从列的角度看是什么意思</font>, 我姑且认为在做的开始, $A$ 和 $B$ 都被认为是一列一列呈现的

$A$就被我们看成从$$

A = \begin{bmatrix} a_{11} & a_{12} & a_{13} & a_{14} \\ a_{21} & a_{22} & a_{23} & a_{24} \\ a_{31} & a_{32} & a_{33} & a_{34} \\ a_{41} & a_{42} & a_{43} & a_{44} \end{bmatrix}
$$
​​​​
列向量视角的 $A$：
$$
A = \left[ \vec{a}_1 \quad \vec{a}_2 \quad \vec{a}_3 \quad \vec{a}_4 \right]
$$

$$ 
\vec{a}_1 = \begin{bmatrix} a_{11} \\ a_{21} \\ a_{31} \\ a_{41} \end{bmatrix}, \quad
\vec{a}_2 = \begin{bmatrix} a_{12} \\ a_{22} \\ a_{32} \\ a_{42} \end{bmatrix}, \quad
\vec{a}_3 = \begin{bmatrix} a_{13} \\ a_{23} \\ a_{33} \\ a_{43} \end{bmatrix}, \quad
\vec{a}_4 = \begin{bmatrix} a_{14} \\ a_{24} \\ a_{34} \\ a_{44} \end{bmatrix}

$$




OK, 我们得到 $A = \left[ \vec{a}_1 \quad \vec{a}_2 \quad \vec{a}_3 \quad \vec{a}_4 \right]$ 后开始处理 $B$ , 同样列向量视角
​​​​
 从$$B = \begin{bmatrix} b_{11} & b_{12} & b_{13} & b_{14} \\ b_{21} & b_{22} & b_{23} & b_{24} \\ b_{31} & b_{32} & b_{33} & b_{34} \\ b_{41} & b_{42} & b_{43} & b_{44} \end{bmatrix}$$
​到
$$B = \left[ \vec{b}_1 \quad \vec{b}_2 \quad \vec{b}_3 \quad \vec{b}_4 \right]$$


$$\vec{b}_1 = \begin{bmatrix} b_{11} \\ b_{21} \\ b_{31} \\ b_{41} \end{bmatrix}, \quad
\vec{b}_2 = \begin{bmatrix} b_{12} \\ b_{22} \\ b_{32} \\ b_{42} \end{bmatrix},
\quad

\vec{b}_3 = \begin{bmatrix} b_{13} \\ b_{23} \\ b_{33} \\ b_{43} \end{bmatrix},
\quad

\vec{b}_4 = \begin{bmatrix} b_{14} \\ b_{24} \\ b_{34} \\ b_{44} \end{bmatrix},
\quad


$$

写完后, 我们的 $B$ 作为之前的数值位置, $A$中的向量都是作为新的坐标系来构建, 那么我们可以得到



## 3. "列中列"展开法的具体表示

矩阵乘积 $C = A \cdot B$ 的完整展开形式：

$$C = \left[ \begin{array}{cccc} b_{11} \cdot \begin{bmatrix} a_{11} \\ a_{21} \\ a_{31} \\ a_{41} \end{bmatrix} + b_{21} \cdot \begin{bmatrix} a_{12} \\ a_{22} \\ a_{32} \\ a_{42} \end{bmatrix} + b_{31} \cdot \begin{bmatrix} a_{13} \\ a_{23} \\ a_{33} \\ a_{43} \end{bmatrix} + b_{41} \cdot \begin{bmatrix} a_{14} \\ a_{24} \\ a_{34} \\ a_{44} \end{bmatrix} & b_{12} \cdot \begin{bmatrix} a_{11} \\ a_{21} \\ a_{31} \\ a_{41} \end{bmatrix} + b_{22} \cdot \begin{bmatrix} a_{12} \\ a_{22} \\ a_{32} \\ a_{42} \end{bmatrix} + b_{32} \cdot \begin{bmatrix} a_{13} \\ a_{23} \\ a_{33} \\ a_{43} \end{bmatrix} + b_{42} \cdot \begin{bmatrix} a_{14} \\ a_{24} \\ a_{34} \\ a_{44} \end{bmatrix} & b_{13} \cdot \begin{bmatrix} a_{11} \\ a_{21} \\ a_{31} \\ a_{41} \end{bmatrix} + b_{23} \cdot \begin{bmatrix} a_{12} \\ a_{22} \\ a_{32} \\ a_{42} \end{bmatrix} + b_{33} \cdot \begin{bmatrix} a_{13} \\ a_{23} \\ a_{33} \\ a_{43} \end{bmatrix} + b_{43} \cdot \begin{bmatrix} a_{14} \\ a_{24} \\ a_{34} \\ a_{44} \end{bmatrix} & b_{14} \cdot \begin{bmatrix} a_{11} \\ a_{21} \\ a_{31} \\ a_{41} \end{bmatrix} + b_{24} \cdot \begin{bmatrix} a_{12} \\ a_{22} \\ a_{32} \\ a_{42} \end{bmatrix} + b_{34} \cdot \begin{bmatrix} a_{13} \\ a_{23} \\ a_{33} \\ a_{43} \end{bmatrix} + b_{44} \cdot \begin{bmatrix} a_{14} \\ a_{24} \\ a_{34} \\ a_{44} \end{bmatrix} \end{array} \right] $$

$\rightarrow$ 

$$ 
\left[ \begin{array}{cccc} \begin{bmatrix} b_{11} a_{11} \\ b_{11} a_{21} \\ b_{11} a_{31} \\ b_{11} a_{41} \end{bmatrix} + \begin{bmatrix} b_{21} a_{12} \\ b_{21} a_{22} \\ b_{21} a_{32} \\ b_{21} a_{42} \end{bmatrix} + \begin{bmatrix} b_{31} a_{13} \\ b_{31} a_{23} \\ b_{31} a_{33} \\ b_{31} a_{43} \end{bmatrix} + \begin{bmatrix} b_{41} a_{14} \\ b_{41} a_{24} \\ b_{41} a_{34} \\ b_{41} a_{44} \end{bmatrix} & \begin{bmatrix} b_{12} a_{11} \\ b_{12} a_{21} \\ b_{12} a_{31} \\ b_{12} a_{41} \end{bmatrix} + \begin{bmatrix} b_{22} a_{12} \\ b_{22} a_{22} \\ b_{22} a_{32} \\ b_{22} a_{42} \end{bmatrix} + \begin{bmatrix} b_{32} a_{13} \\ b_{32} a_{23} \\ b_{32} a_{33} \\ b_{32} a_{43} \end{bmatrix} + \begin{bmatrix} b_{42} a_{14} \\ b_{42} a_{24} \\ b_{42} a_{34} \\ b_{42} a_{44} \end{bmatrix} & \begin{bmatrix} b_{13} a_{11} \\ b_{13} a_{21} \\ b_{13} a_{31} \\ b_{13} a_{41} \end{bmatrix} + \begin{bmatrix} b_{23} a_{12} \\ b_{23} a_{22} \\ b_{23} a_{32} \\ b_{23} a_{42} \end{bmatrix} + \begin{bmatrix} b_{33} a_{13} \\ b_{33} a_{23} \\ b_{33} a_{33} \\ b_{33} a_{43} \end{bmatrix} + \begin{bmatrix} b_{43} a_{14} \\ b_{43} a_{24} \\ b_{43} a_{34} \\ b_{43} a_{44} \end{bmatrix} & \begin{bmatrix} b_{14} a_{11} \\ b_{14} a_{21} \\ b_{14} a_{31} \\ b_{14} a_{41} \end{bmatrix} + \begin{bmatrix} b_{24} a_{12} \\ b_{24} a_{22} \\ b_{24} a_{32} \\ b_{24} a_{42} \end{bmatrix} + \begin{bmatrix} b_{34} a_{13} \\ b_{34} a_{23} \\ b_{34} a_{33} \\ b_{34} a_{43} \end{bmatrix} + \begin{bmatrix} b_{44} a_{14} \\ b_{44} a_{24} \\ b_{44} a_{34} \\ b_{44} a_{44} \end{bmatrix} \end{array} \right]
$$ 
$\rightarrow$ 

其中我们拿出一条来
$$ b_{11} \cdot \begin{bmatrix} a_{11} \\ a_{21} \\ a_{31} \\ a_{41} \end{bmatrix} + b_{21} \cdot \begin{bmatrix} a_{12} \\ a_{22} \\ a_{32} \\ a_{42} \end{bmatrix} + b_{31} \cdot \begin{bmatrix} a_{13} \\ a_{23} \\ a_{33} \\ a_{43} \end{bmatrix} + b_{41} \cdot \begin{bmatrix} a_{14} \\ a_{24} \\ a_{34} \\ a_{44} \end{bmatrix} $$
是这样的, 
$$ 
\begin{bmatrix} b_{11}a_{11} \\ b_{11}a_{21} \\ b_{11}a_{31} \\ b_{11}a_{41} \end{bmatrix} + \begin{bmatrix} b_{21}a_{12} \\ b_{21}a_{22} \\ b_{21}a_{32} \\ b_{21}a_{42} \end{bmatrix} + \begin{bmatrix} b_{31} a_{13} \\ b_{31}a_{23} \\ b_{31} a_{33} \\ b_{31} a_{43} \end{bmatrix} +\begin{bmatrix} b_{41}a_{14} \\ b_{41}a_{24} \\ b_{41}a_{34} \\ b_{41}a_{44} \end{bmatrix} 
$$

再线性相加
$$
= \begin{bmatrix} b_{11}a_{11} + b_{21}a_{12} + b_{31}a_{13} + b_{41}a_{14} \\ b_{11}a_{21} + b_{21}a_{22} + b_{31}a_{23} + b_{41}a_{24} \\ b_{11}a_{31} + b_{21}a_{32} + b_{31}a_{33} + b_{41}a_{34} \\ b_{11}a_{41} + b_{21}a_{42} + b_{31}a_{43} + b_{41}a_{44} \end{bmatrix}
$$

这是一个$4\times 1$的矩阵, 然后我们有4条, 最后是 一个$4\times 4$ 的结果

$$\begin{bmatrix} a_{11} b_{11} + a_{12} b_{21} + a_{13} b_{31} + a_{14} b_{41} & a_{11} b_{12} + a_{12} b_{22} + a_{13} b_{32} + a_{14} b_{42} & a_{11} b_{13} + a_{12} b_{23} + a_{13} b_{33} + a_{14} b_{43} & a_{11} b_{14} + a_{12} b_{24} + a_{13} b_{34} + a_{14} b_{44} \\ a_{21} b_{11} + a_{22} b_{21} + a_{23} b_{31} + a_{24} b_{41} & a_{21} b_{12} + a_{22} b_{22} + a_{23} b_{32} + a_{24} b_{42} & a_{21} b_{13} + a_{22} b_{23} + a_{23} b_{33} + a_{24} b_{43} & a_{21} b_{14} + a_{22} b_{24} + a_{23} b_{34} + a_{24} b_{44} \\ a_{31} b_{11} + a_{32} b_{21} + a_{33} b_{31} + a_{34} b_{41} & a_{31} b_{12} + a_{32} b_{22} + a_{33} b_{32} + a_{34} b_{42} & a_{31} b_{13} + a_{32} b_{23} + a_{33} b_{33} + a_{34} b_{43} & a_{31} b_{14} + a_{32} b_{24} + a_{33} b_{34} + a_{34} b_{44} \\ a_{41} b_{11} + a_{42} b_{21} + a_{43} b_{31} + a_{44} b_{41} & a_{41} b_{12} + a_{42} b_{22} + a_{43} b_{32} + a_{44} b_{42} & a_{41} b_{13} + a_{42} b_{23} + a_{43} b_{33} + a_{44} b_{43} & a_{41} b_{14} + a_{42} b_{24} + a_{43} b_{34} + a_{44} b_{44} \end{bmatrix}
$$


这时候有一些经典的问题, 就是从这个转动的性质出发了

1. **矩阵相乘是否满足交换率?** 当然不行, 都完全是两个东西了

2. **矩阵相乘成立的条件是前一个matrix的什么要等于后一个matrix的什么?** 完全不用急, 想着 $Ax = b$ 在这个时候,  $A$ 是我们的旋转/变换系统, 想象每一列都是独立的, rank是满秩的(其实不用只要操作的时候有那个维度就OK了), 那么在这个情况下, 我们的 $x$ 中的 $[x_1 \dots x_n]$ 当然是要和前面的 $A$ 有多少列要匹配了

3. <font color='red'>这里理解错了, 说明有知识点没懂</font> $Ax = b$ 中的 b是 几乘几点结果, 感觉x的维度是怎样, b就长怎样? 如果从 $A$ 是提供旋转功能的角度出发的话, 为什么会因为旋转 b相比原先旋转的对象 x 增加维度呢?
	这其实是更广义的「**线性变换**」，不仅仅是旋转, 不一定是严格的旋转，它可以是 **旋转 + 拉伸**(放大缩小) 投影 (把高维变低维) 嵌入 (把低维映射到高维) 剪切(shear)
	
4. **如果说 3 by 2的matrix, 如何0.5s内说出 2 是2行还是2列?** 之前我是使用行列式这样的背住然后套的, 但是这里提供一种更加直觉的想法, 是, 我们定义这个名字的时候, 更加关注输出, 什么是输出, 变换后矩阵的维度, 那么变换后矩阵的维度是什么, 是由什么确定的, 这样想下去就是, 当然是  $A$ 这个提供变换的方案的matrix确定, 然后再想象一下, 这里的A的维度是什么, 是A的行数(row), 因为我们考虑的是A每一列vector的维度, 这样我们这个变化系统的row就确定了, 所以3 by 2的matrix的话, 3 $\rightarrow$  row, 所以是3 行 2 列的矩阵. 


**未完待续**
1. 矩阵乘法的剩下三种理解方法
2. 变化的特色case, 为什么有些乘上有些矩阵的时候, 在一个维度上没有变动
3. 第二个问题在看3Blue1Brown发现他希望不动的x维度上, 对应的 A的位置, 好像都是单位矩阵的part, 虽然不知道再哪个位置(哪一层)放1
4. 之后要详细讨论的点是, 在3这个视频中, 所谓的 单个 $A$ 矩阵如果是变换作用的话, 居然直接是单位矩阵想要最后变成的固定状态(停在那个位置). 
5. 左乘看成新坐标系的基向量，右边的原向量看成标量
## 标准基底下的矢量

<svg width="400" height="400" viewBox="-100 -100 200 200" xmlns="http://www.w3.org/2000/svg">
  <!-- 网格线 -->
  <g stroke="#ccc" stroke-width="0.5">
    <!-- 纵向 -->
    <line x1="-90" y1="-100" x2="-90" y2="100"/>
    <line x1="-80" y1="-100" x2="-80" y2="100"/>
    <line x1="-70" y1="-100" x2="-70" y2="100"/>
    <line x1="-60" y1="-100" x2="-60" y2="100"/>
    <line x1="-50" y1="-100" x2="-50" y2="100"/>
    <line x1="-40" y1="-100" x2="-40" y2="100"/>
    <line x1="-30" y1="-100" x2="-30" y2="100"/>
    <line x1="-20" y1="-100" x2="-20" y2="100"/>
    <line x1="-10" y1="-100" x2="-10" y2="100"/>
    <line x1="10" y1="-100" x2="10" y2="100"/>
    <line x1="20" y1="-100" x2="20" y2="100"/>
    <line x1="30" y1="-100" x2="30" y2="100"/>
    <line x1="40" y1="-100" x2="40" y2="100"/>
    <line x1="50" y1="-100" x2="50" y2="100"/>
    <line x1="60" y1="-100" x2="60" y2="100"/>
    <line x1="70" y1="-100" x2="70" y2="100"/>
    <line x1="80" y1="-100" x2="80" y2="100"/>
    <line x1="90" y1="-100" x2="90" y2="100"/>
    <!-- 横向 -->
    <line x1="-100" y1="-90" x2="100" y2="-90"/>
    <line x1="-100" y1="-80" x2="100" y2="-80"/>
    <line x1="-100" y1="-70" x2="100" y2="-70"/>
    <line x1="-100" y1="-60" x2="100" y2="-60"/>
    <line x1="-100" y1="-50" x2="100" y2="-50"/>
    <line x1="-100" y1="-40" x2="100" y2="-40"/>
    <line x1="-100" y1="-30" x2="100" y2="-30"/>
    <line x1="-100" y1="-20" x2="100" y2="-20"/>
    <line x1="-100" y1="-10" x2="100" y2="-10"/>
    <line x1="-100" y1="10" x2="100" y2="10"/>
    <line x1="-100" y1="20" x2="100" y2="20"/>
    <line x1="-100" y1="30" x2="100" y2="30"/>
    <line x1="-100" y1="40" x2="100" y2="40"/>
    <line x1="-100" y1="50" x2="100" y2="50"/>
    <line x1="-100" y1="60" x2="100" y2="60"/>
    <line x1="-100" y1="70" x2="100" y2="70"/>
    <line x1="-100" y1="80" x2="100" y2="80"/>
    <line x1="-100" y1="90" x2="100" y2="90"/>
  </g>

  <!-- 坐标轴 -->
  <line x1="-100" y1="0" x2="100" y2="0" stroke="black" stroke-width="1"/>
  <line x1="0" y1="-100" x2="0" y2="100" stroke="black" stroke-width="1"/>

  <!-- 标准基底 i -->
  <line x1="0" y1="0" x2="20" y2="0" stroke="green" stroke-width="2" marker-end="url(#arrow-green)"/>
  <text x="22" y="0" fill="green" font-size="12">î (1,0)</text>

  <!-- 标准基底 j -->
  <line x1="0" y1="0" x2="0" y2="-20" stroke="red" stroke-width="2" marker-end="url(#arrow-red)"/>
  <text x="2" y="-22" fill="red" font-size="12">ĵ (0,1)</text>

  <!-- 原始矢量 v = (1,2) -->
  <line x1="0" y1="0" x2="20" y2="-40" stroke="orange" stroke-width="2" marker-end="url(#arrow-orange)"/>
  <text x="22" y="-42" fill="orange" font-size="12">v (1,2)</text>

  <!-- 箭头定义 -->
  <defs>
    <marker id="arrow-green" markerWidth="4" markerHeight="4" refX="3" refY="2" orient="auto">
      <path d="M0,0 L4,2 L0,4 Z" fill="green"/>
    </marker>
    <marker id="arrow-red" markerWidth="4" markerHeight="4" refX="3" refY="2" orient="auto">
      <path d="M0,0 L4,2 L0,4 Z" fill="red"/>
    </marker>
    <marker id="arrow-orange" markerWidth="4" markerHeight="4" refX="3" refY="2" orient="auto">
      <path d="M0,0 L4,2 L0,4 Z" fill="orange"/>
    </marker>
  </defs>
</svg>

## 变换基底后的矢量

<svg width="400" height="400" viewBox="-100 -100 200 200" xmlns="http://www.w3.org/2000/svg">
<!-- 网格线 -->
  <g stroke="#ccc" stroke-width="0.5">
    <!-- 纵向 -->
    <line x1="-90" y1="-100" x2="-90" y2="100"/>
    <line x1="-80" y1="-100" x2="-80" y2="100"/>
    <line x1="-70" y1="-100" x2="-70" y2="100"/>
    <line x1="-60" y1="-100" x2="-60" y2="100"/>
    <line x1="-50" y1="-100" x2="-50" y2="100"/>
    <line x1="-40" y1="-100" x2="-40" y2="100"/>
    <line x1="-30" y1="-100" x2="-30" y2="100"/>
    <line x1="-20" y1="-100" x2="-20" y2="100"/>
    <line x1="-10" y1="-100" x2="-10" y2="100"/>
    <line x1="10" y1="-100" x2="10" y2="100"/>
    <line x1="20" y1="-100" x2="20" y2="100"/>
    <line x1="30" y1="-100" x2="30" y2="100"/>
    <line x1="40" y1="-100" x2="40" y2="100"/>
    <line x1="50" y1="-100" x2="50" y2="100"/>
    <line x1="60" y1="-100" x2="60" y2="100"/>
    <line x1="70" y1="-100" x2="70" y2="100"/>
    <line x1="80" y1="-100" x2="80" y2="100"/>
    <line x1="90" y1="-100" x2="90" y2="100"/>
    <!-- 横向 -->
    <line x1="-100" y1="-90" x2="100" y2="-90"/>
    <line x1="-100" y1="-80" x2="100" y2="-80"/>
    <line x1="-100" y1="-70" x2="100" y2="-70"/>
    <line x1="-100" y1="-60" x2="100" y2="-60"/>
    <line x1="-100" y1="-50" x2="100" y2="-50"/>
    <line x1="-100" y1="-40" x2="100" y2="-40"/>
    <line x1="-100" y1="-30" x2="100" y2="-30"/>
    <line x1="-100" y1="-20" x2="100" y2="-20"/>
    <line x1="-100" y1="-10" x2="100" y2="-10"/>
    <line x1="-100" y1="10" x2="100" y2="10"/>
    <line x1="-100" y1="20" x2="100" y2="20"/>
    <line x1="-100" y1="30" x2="100" y2="30"/>
    <line x1="-100" y1="40" x2="100" y2="40"/>
    <line x1="-100" y1="50" x2="100" y2="50"/>
    <line x1="-100" y1="60" x2="100" y2="60"/>
    <line x1="-100" y1="70" x2="100" y2="70"/>
    <line x1="-100" y1="80" x2="100" y2="80"/>
    <line x1="-100" y1="90" x2="100" y2="90"/>
  </g>


  <!-- 坐标轴 -->
  <line x1="-100" y1="0" x2="100" y2="0" stroke="black" stroke-width="1"/>
  <line x1="0" y1="-100" x2="0" y2="100" stroke="black" stroke-width="1"/>

  <!-- 新基底 i -->
  <line x1="0" y1="0" x2="20" y2="0" stroke="green" stroke-width="2" marker-end="url(#arrow-green)"/>
  <text x="22" y="0" fill="green" font-size="12">î' (1,0)</text>

  <!-- 新基底 j -->
  <line x1="0" y1="0" x2="20" y2="-20" stroke="red" stroke-width="2" marker-end="url(#arrow-red)"/>
  <text x="22" y="-22" fill="red" font-size="12">ĵ' (1,1)</text>

  <!-- 变换后的矢量 v' = (3,2) -->
  <line x1="0" y1="0" x2="60" y2="-40" stroke="orange" stroke-width="2" marker-end="url(#arrow-orange)"/>
  <text x="62" y="-42" fill="orange" font-size="12">v' (3,2)</text>

  <!-- 箭头定义 -->
  <defs>
    <marker id="arrow-green" markerWidth="4" markerHeight="4" refX="3" refY="2" orient="auto">
      <path d="M0,0 L4,2 L0,4 Z" fill="green"/>
    </marker>
    <marker id="arrow-red" markerWidth="4" markerHeight="4" refX="3" refY="2" orient="auto">
      <path d="M0,0 L4,2 L0,4 Z" fill="red"/>
    </marker>
    <marker id="arrow-orange" markerWidth="4" markerHeight="4" refX="3" refY="2" orient="auto">
      <path d="M0,0 L4,2 L0,4 Z" fill="orange"/>
    </marker>
  </defs>
</svg>

5. 还有细节是对于提供变化的matrix $\begin{bmatrix} -1 & 4 \\ 1 & 2 \end{bmatrix}$ , 我们可以直接认为其中$\begin{bmatrix} -1  \\ 1  \end{bmatrix}$ 就是 unit vector $i$ 的新位置, 而$\begin{bmatrix} 4 \\2 \end{bmatrix}$ 就是 unit vector $j$ 的新位置

### #  Chapter 4, Essence of linear algebra, Chapter 5 说了一下三维, 没讲什么
章节中对于$x$ 多维过程计算一个batch的过程, 其实就是拆开一步步的过程

$$ \begin{align*}
&\underset{M_2}{\begin{bmatrix} \textcolor{purple}0 & \textcolor{purple}2 \\ \textcolor{purple}1 & \textcolor{purple}0 \end{bmatrix}} 
\cdot 
\underset{M_1}{\begin{bmatrix} 
\color{green}{1} & \color{orange}{-2} \\ 
\color{green}{1} & \color{orange}{0} 
\end{bmatrix}} 
= 
\begin{bmatrix} 
? & ? \\ 
? & ? 
\end{bmatrix} 
\\[10pt]

&\begin{bmatrix} 
\textcolor{purple}0 & \textcolor{purple}2 \\ 
\textcolor{purple}1 & \textcolor{purple}0 
\end{bmatrix} 
\cdot 
\begin{bmatrix} 
\color{green}{1}\\ 
\color{green}{1}
\end{bmatrix} 
= \textcolor{green}{1} \cdot \begin{bmatrix} 
\textcolor{purple}0 \\ 
\textcolor{purple}1
\end{bmatrix} 
+ 
\textcolor{green}{1} \cdot 
\begin{bmatrix} 
\textcolor{purple}2 \\ 
\textcolor{purple}0 
\end{bmatrix} 
= 
\begin{bmatrix} 
2 \\ 
1 
\end{bmatrix}
\end{align*}
$$ 
我们得出 $\rightarrow$ 
$$
\begin{align*}
&\underset{M_2}{\begin{bmatrix} \textcolor{purple}0 & \textcolor{purple}2 \\ \textcolor{purple}1 & \textcolor{purple}0 \end{bmatrix}} 
\cdot 
\underset{M_1}{\begin{bmatrix} 
\color{green}{1} & \color{orange}{-2} \\ 
\color{green}{1} & \color{orange}{0} 
\end{bmatrix}} 
= 
\begin{bmatrix} 
2 & ? \\ 
1 & ? 
\end{bmatrix} 
\\[10pt]
\end{align*}

$$
这里其实有一个小疑惑, 就是$ABCDEF \cdot x$ 中, 第一个$F$, 对于 $x$ 的坐标映射, 是不是就是遵循$F$ 中的样子来就可以了, 但是对于剩下的步骤, 因为大概率不orthogonal, 所以其实多维的都有影响?





### 1. 矩阵乘法的剩下三种理解方法

图设计来自[gwave](https://www.zhihu.com/people/gwave-22) 知乎答主, 使用svg重新绘制, 突出版权, 在重制中仍然保留水印.


**矩阵-向量乘法-列视角：矩阵右乘列向量，向量对矩阵的列进行线性组合**
<svg viewBox="0 0 600 200" xmlns="http://www.w3.org/2000/svg">
  <!-- 3x3 矩阵列块 -->
  <!-- 红列 -->
  <rect x="10" y="50" width="30" height="30" fill="#e57373" stroke="black" stroke-width="1"/>
  <rect x="10" y="80" width="30" height="30" fill="#e57373" stroke="black" stroke-width="1"/>
  <rect x="10" y="110" width="30" height="30" fill="#e57373" stroke="black" stroke-width="1"/>
  <!-- 绿列 -->
  <rect x="40" y="50" width="30" height="30" fill="#81c784" stroke="black" stroke-width="1"/>
  <rect x="40" y="80" width="30" height="30" fill="#81c784" stroke="black" stroke-width="1"/>
  <rect x="40" y="110" width="30" height="30" fill="#81c784" stroke="black" stroke-width="1"/>
  <!-- 蓝列 -->
  <rect x="70" y="50" width="30" height="30" fill="#64b5f6" stroke="black" stroke-width="1"/>
  <rect x="70" y="80" width="30" height="30" fill="#64b5f6" stroke="black" stroke-width="1"/>
  <rect x="70" y="110" width="30" height="30" fill="#64b5f6" stroke="black" stroke-width="1"/>
  
  <!-- 乘号 × -->
  <text x="110" y="105" font-size="24" font-family="Arial">×</text>
  
  <!-- 列向量 a b c -->
  <rect x="140" y="50" width="30" height="30" fill="white" stroke="black" stroke-width="1"/>
  <text x="150" y="70" font-size="16" font-family="Arial">a</text>
  <rect x="140" y="80" width="30" height="30" fill="white" stroke="black" stroke-width="1"/>
  <text x="150" y="100" font-size="16" font-family="Arial">b</text>
  <rect x="140" y="110" width="30" height="30" fill="white" stroke="black" stroke-width="1"/>
  <text x="150" y="130" font-size="16" font-family="Arial">c</text>
  
  <!-- 等号 -->
  <text x="180" y="105" font-size="24" font-family="Arial">=</text>
  
  <!-- a * 红列 -->
  <rect x="230" y="50" width="30" height="30" fill="#e57373" stroke="black" stroke-width="1"/>
  <rect x="230" y="80" width="30" height="30" fill="#e57373" stroke="black" stroke-width="1"/>
  <rect x="230" y="110" width="30" height="30" fill="#e57373" stroke="black" stroke-width="1"/>
  <!-- a 方块在左侧，不覆盖 -->
  <rect x="200" y="80" width="30" height="30" fill="white" stroke="black" stroke-width="1"/>
  <text x="210" y="100" font-size="16" font-family="Arial">a</text>
  
  <!-- 加号 -->
  <text x="270" y="105" font-size="24" font-family="Arial">+</text>
  
  <!-- b * 绿列 -->
  <rect x="320" y="50" width="30" height="30" fill="#81c784" stroke="black" stroke-width="1"/>
  <rect x="320" y="80" width="30" height="30" fill="#81c784" stroke="black" stroke-width="1"/>
  <rect x="320" y="110" width="30" height="30" fill="#81c784" stroke="black" stroke-width="1"/>
  <!-- b 方块在左侧，不覆盖 -->
  <rect x="290" y="80" width="30" height="30" fill="white" stroke="black" stroke-width="1"/>
  <text x="300" y="100" font-size="16" font-family="Arial">b</text>
  
  <!-- 加号 -->
  <text x="360" y="105" font-size="24" font-family="Arial">+</text>
  
  <!-- c * 蓝列 -->
  <rect x="410" y="50" width="30" height="30" fill="#64b5f6" stroke="black" stroke-width="1"/>
  <rect x="410" y="80" width="30" height="30" fill="#64b5f6" stroke="black" stroke-width="1"/>
  <rect x="410" y="110" width="30" height="30" fill="#64b5f6" stroke="black" stroke-width="1"/>
  <!-- c 方块在左侧，不覆盖 -->
  <rect x="380" y="80" width="30" height="30" fill="white" stroke="black" stroke-width="1"/>
  <text x="390" y="100" font-size="16" font-family="Arial">c</text>
  
  <!-- 等号 -->
  <text x="450" y="105" font-size="24" font-family="Arial">=</text>
  
  <!-- 最终结果 粉灰色条 -->
  <rect x="480" y="50" width="30" height="30" fill="#f8bbd0" stroke="black" stroke-width="1"/>
  <rect x="480" y="80" width="30" height="30" fill="#f8bbd0" stroke="black" stroke-width="1"/>
  <rect x="480" y="110" width="30" height="30" fill="#f8bbd0" stroke="black" stroke-width="1"/>
  
  <!-- 右下角水印 -->
  <text x="420" y="170" font-size="14" fill="#666">知乎 @waywa</text>
</svg>
**矩阵-向量乘法-行视角：矩阵左乘行向量，向量对矩阵的行进行线性组合**
<svg viewBox="0 0 700 230" xmlns="http://www.w3.org/2000/svg">
  <!-- 左侧 行向量 a b c -->
  <rect x="20" y="100" width="30" height="30" fill="white" stroke="black" stroke-width="1"/>
  <text x="30" y="120" font-size="16" font-family="Arial">a</text>
  <rect x="50" y="100" width="30" height="30" fill="white" stroke="black" stroke-width="1"/>
  <text x="60" y="120" font-size="16" font-family="Arial">b</text>
  <rect x="80" y="100" width="30" height="30" fill="white" stroke="black" stroke-width="1"/>
  <text x="90" y="120" font-size="16" font-family="Arial">c</text>
  
  <!-- 乘号 × - 与第一个图保持一致的大小 -->
  <text x="125" y="125" font-size="24" font-family="Arial">×</text>
  
  <!-- 3x3 矩阵列块 -->
  <!-- 红行 -->
  <rect x="160" y="70" width="30" height="30" fill="#e57373" stroke="black" stroke-width="1"/>
  <rect x="190" y="70" width="30" height="30" fill="#e57373" stroke="black" stroke-width="1"/>
  <rect x="220" y="70" width="30" height="30" fill="#e57373" stroke="black" stroke-width="1"/>
  <!-- 绿行 -->
  <rect x="160" y="100" width="30" height="30" fill="#81c784" stroke="black" stroke-width="1"/>
  <rect x="190" y="100" width="30" height="30" fill="#81c784" stroke="black" stroke-width="1"/>
  <rect x="220" y="100" width="30" height="30" fill="#81c784" stroke="black" stroke-width="1"/>
  <!-- 蓝行 -->
  <rect x="160" y="130" width="30" height="30" fill="#64b5f6" stroke="black" stroke-width="1"/>
  <rect x="190" y="130" width="30" height="30" fill="#64b5f6" stroke="black" stroke-width="1"/>
  <rect x="220" y="130" width="30" height="30" fill="#64b5f6" stroke="black" stroke-width="1"/>
  
  <!-- 等号 - 与第一个图保持一致的大小 -->
  <text x="290" y="125" font-size="24" font-family="Arial">=</text>
  
  <!-- 右侧计算过程 -->
  <!-- a * 红行 -->
  <rect x="340" y="40" width="30" height="30" fill="white" stroke="black" stroke-width="1"/>
  <text x="350" y="60" font-size="16" font-family="Arial">a</text>
  <rect x="370" y="40" width="30" height="30" fill="#e57373" stroke="black" stroke-width="1"/>
  <rect x="400" y="40" width="30" height="30" fill="#e57373" stroke="black" stroke-width="1"/>
  <rect x="430" y="40" width="30" height="30" fill="#e57373" stroke="black" stroke-width="1"/>
  
  <!-- 加号（a和b之间） - 保持一致大小 -->
  <text x="380" y="95" font-size="24" font-family="Arial">+</text>
  
  <!-- b * 绿行 -->
  <rect x="340" y="100" width="30" height="30" fill="white" stroke="black" stroke-width="1"/>
  <text x="350" y="120" font-size="16" font-family="Arial">b</text>
  <rect x="370" y="100" width="30" height="30" fill="#81c784" stroke="black" stroke-width="1"/>
  <rect x="400" y="100" width="30" height="30" fill="#81c784" stroke="black" stroke-width="1"/>
  <rect x="430" y="100" width="30" height="30" fill="#81c784" stroke="black" stroke-width="1"/>
  
  <!-- 加号（b和c之间） - 保持一致大小 -->
  <text x="380" y="155" font-size="24" font-family="Arial">+</text>
  
  <!-- c * 蓝行 -->
  <rect x="340" y="160" width="30" height="30" fill="white" stroke="black" stroke-width="1"/>
  <text x="350" y="180" font-size="16" font-family="Arial">c</text>
  <rect x="370" y="160" width="30" height="30" fill="#64b5f6" stroke="black" stroke-width="1"/>
  <rect x="400" y="160" width="30" height="30" fill="#64b5f6" stroke="black" stroke-width="1"/>
  <rect x="430" y="160" width="30" height="30" fill="#64b5f6" stroke="black" stroke-width="1"/>
  
  <!-- 最后等号 - 保持一致大小 -->
  <text x="480" y="125" font-size="24" font-family="Arial">=</text>
  
  <!-- 最终结果 粉色行 -->
  <rect x="520" y="100" width="30" height="30" fill="#f8bbd0" stroke="black" stroke-width="1"/>
  <rect x="550" y="100" width="30" height="30" fill="#f8bbd0" stroke="black" stroke-width="1"/>
  <rect x="580" y="100" width="30" height="30" fill="#f8bbd0" stroke="black" stroke-width="1"/>
  
  <!-- 右下角水印 -->
  <text x="520" y="210" font-size="14" fill="#666">知乎 @waywa</text>
</svg>
还没理解完, 未完待续 

## RREF(Reduced Row-Echelon Form)

感觉是一个很小的概念不在ML中常用到, 
意思是“是不是高斯消元法最后让每个基向量尽可能简单”，那可以说是的。每一行代表一个单位基方向，其他方向全0, 可以理解成“最小单位向量”，但其实数学上是标准基, 但是注意，它们不一定是整个空间的 unit vector，而是 **在矩阵的列空间或行空间中**形成了一个基底。

彼此线性无关，数量就是行空间的维度，也就是矩阵的秩。
列空间的秩=行空间的秩, 这个概念好像是**有点背的**, 还有下面这个公式
$$
rank(A)=rank(A^\top)
$$
秩，GPT说其实代表这个系统“真正有多复杂”，而不是表面的行和列数量。








**Reference**

矩阵乘法核心思想（2）：行空间 - *gwave* 知乎 https://zhuanlan.zhihu.com/p/348551903
Essence of linear algebra *3Blue1Brown*  https://youtu.be/fNk_zzaMoSs?si=UlVZ_LHcoih4kQvu
NTU 线性代数 Hung-yi Lee (李宏毅) https://googly-mingto.github.io/LA_2022_fall/2022-fall.html
MIT18.06 Linear-Algebra  https://ocw.mit.edu/courses/18-06-linear-algebra-spring-2010/