---
layout: post
title:  "Proof of Cramer’s Rule"
date: 2023-08-02
---

The article contains three proofs.

## 证明一

**证明**：假设A是一个可逆的n × n矩阵，我们考虑线性系统AX = b。这个系统有一个唯一的解：

<font color='red'>转换不了解，第二步转换</font> <font color='blue'>感觉是基础问题不知道</font> 
$$
X = A^{-1}b = \frac{1}{|A|}\text{adj}(A) \cdot b = \frac{1}{|A|} \left[ \begin{array}{cccc} A_{11} & A_{21} & \cdots & A_{n1} \\ \vdots & \vdots & \ddots & \vdots \\ A_{1n} & A_{2n} & \cdots & A_{nn} \end{array} \right] b
$$

这里的 $\cdot$ 表示矩阵乘法。通过矩阵乘法的公式，第k个未知数$x_k$可以写成：

$$
x_k = \frac{1}{|A|} \sum_{i=1}^{n} A_{ik}b_i = \frac{1}{|A|} \text{det} [c_1, \ldots, c_{k-1}, b, c_{k+1}, \ldots, c_n]
$$

这里$c_i$表示A的第i列。第二个等式来自于对矩阵 $[c_1, \ldots, c_{k-1}, b, c_{k+1}, \ldots, c_n]$ 沿第k列进行的余子式展开。



## 证明二

首先，假设我们有一个可逆的矩阵$A$，且$\det(A) \neq 0$，并且$Ax = b$是一个线性方程。我们声明这个方程有一个唯一解。注意到$A^{-1}b$是一个解，因为$A(A^{-1}b) = (AA^{-1})b = b$，所以解是存在的。

假设$s$是这个方程的一个任意解，所以$As = b$。但是，我们可以得到$s = (A^{-1}A)s = A^{-1}(As) = A^{-1}b$，所以$A^{-1}b$是唯一的解。

对于每一个整数$i, 1 \leq i \leq n$，让$a_i$表示$A$的第$i$列，$e_i$表示单位矩阵$I_n$的第$i$列，并且让$X_i$表示从$I_n$通过替换第$i$列为列向量$x$得到的矩阵。

我们知道对于任意的矩阵$A, B$，乘积$AB$的第$k$列是$A$和$B$的第$k$列的乘积。同时，观察到$Ae_k = a_k$对于$k = 1, ..., n$。因此，通过乘法，我们有：

$$
\begin{aligned}
A X_i & =A\left(e_1, \ldots, e_{i-1}, x, e_{i+1}, \ldots, e_n\right) \\
& =\left(A e_1, \ldots, A e_{i-1}, A x, A e_{i+1}, \ldots, A e_n\right) \\
& =\left(a_1, \ldots, a_{i-1}, b, a_{i+1}, \ldots, a_n\right) \\
& =M_i
\end{aligned}
$$


<font color='red'>因为$X_i$是用$x$替换了$I_n$的第$i$列，通过余子式展开计算$X_i$的行列式我们得到</font> ：
$$
det(X_i) = (-1)^{i+i}x_i\det(I_{n-1}) = 1 \cdot x_i \cdot 1 = x_i
$$



因此，根据行列式的乘法性质，我们有
$$
det(M_i) = \det(AX_i) = \det(A)\det(X_i) = \det(A)x_i
$$



所以，$x_i = \frac{\det(M_i)}{\det(A)}$，这就是我们所需要的。



## 证明三

### 形式化总结



线性方程的矩阵表示
$$
Ax=c
$$
其中，系数矩阵 $A$ 是一个$  n×n$ 的方阵，$ x=(x_1,x_2,\cdots,x_n)^T$是一个长度为$n$ 的列向量，$c= (c_1,c_2,\cdots, C_n)^T$也是一个长度为n的列向量。



根据克拉默法则，方程的解为：
$$
x_i=\frac{D_i}{D},i=1,2,\cdots,n
$$


其中， $Di$ 是用 $C$替换了$A$ 的第$i$列得到的矩阵的行列式,$D$则是$A$的行列式。可以看到，当$D$等于0时，原方程无解。

### 证明过程



将线性方程组 $A x=c$ 两边同时左乘 $A$ 的逆, 得到 $A^{-1} A x=A^{-1} c$, 即：
$$
x=A^{-1} c \text { 。 }
$$
我们将系数矩阵表示成列向量的形式, 即:
$$
A=\left(p_1, p_2, \ldots, p_n\right)
$$
因此原方程又可以写成:
$$
\sum_{k=1}^n x_k p_k=c
$$
则行列式 $D_i$ 的值可以表示为:<font color='red'>第二个等号到第三个等号，可以理解为行和列等价，提出一个scalar？</font> 
$$
\begin{aligned}
D_i & =\operatorname{det}\left(p_1, \ldots, p_{i-1}, c, p_{i+1} \ldots, p_n\right) \\
& =\operatorname{det}\left(p_1, \ldots, p_{i-1}, \sum_{k=1}^n x_k p_k, p_{i+1} \ldots, p_n\right) \\
& =\sum_{k=1}^n x_k \operatorname{det}\left(p_1, \ldots, p_{i-1}, p_k, p_{i+1} \ldots, p_n\right) \\
& =x_1 \operatorname{det}\left(p_1, \ldots, p_{i-1}, p_1, p_{i+1} \ldots, p_n\right)+x_2 \operatorname{det}\left(p_1, \ldots, p_{i-1}, p_2, p_{i+1} \ldots, p_n\right)+\ldots \\
& \quad+x_n \operatorname{det}\left(p_1, \ldots, p_{i-1}, p_n, p_{i+1} \ldots, p_n\right) \\
& =x_i \cdot \operatorname{det}(A) \quad \\
& =x_i \cdot D \quad
\end{aligned}
$$
所以 $x_i=\frac{D_i}{D}$ 



## 总结

#### **克拉默法则的表述**

数域 $K$ 上 $\mathrm{n}$ 个方程的 $\mathrm{n}$ 元线性方程组有唯一解的充要条件 $|A| \neq 0$, 且解为 $\left(\frac{\left|B_1\right|}{|A|}, \frac{\left|B_2\right|}{|A|}, \cdots, \frac{\left|B_n\right|}{|A|}\right)$, 其中 $B_i$ 为用常数列替换 $A$ 第i列后的矩阵。

#### 线性空间角度

若 $\alpha_1, \alpha_2, \ldots, \alpha_n$ 是 $K^n$ 的一组基, $\beta \in K^n$ ，则 $\beta=\sum_{i=1}^n \frac{\left|B_i\right|}{|A|} \alpha_i$ 。



#### 问题 如何理解这一结果?

1. $\frac{\left|B_i\right|}{|A|}$ 有什么意义?
2. 行列式有什么意义?
3. 为什么是 $\frac{\left|B_i\right|}{|A|}$ ?
4. 对任意线性空间是否成立类似的结论?
5. 能否类比定义域 $F$ 上的线性空间 $V$ 上的行列式 $\Delta: V^n \rightarrow F$, 从而有类似结论?

​	

### 几何角度


在 $K^n$ 中将一标架作非退化仿射变换 $\sigma$ :
$$
\left\{\begin{array}{c}
K^n \rightarrow K^n \\
\left\{x_1, x_2, \ldots, x_n\right\} \mapsto\left\{\sum_{j=1}^n f_1\left(\alpha_j\right), \sum_{j=1}^n f_2\left(\alpha_j\right), \ldots, \sum_{j=1}^n f_n\left(\alpha_j\right)\right\}
\end{array}\right.
$$
,设 $\delta=\left(x_1, x_2, \ldots, x_n\right)^T$, 即坐标变换公式: $\delta=A \delta^{\prime}$, 那么有 $\delta^{\prime}=\left(\frac{\left|B_1\right|}{|A|}, \frac{\left|B_2\right|}{|A|}, \ldots, \frac{\left|B_n\right|}{|A|}\right)^T$

#### 表层意义

也就是说, 克拉默法则的几何理解就是它给出了非退化仿射变换变换后的新坐标公式。有了这个工具, 在做非退化仿射变换的时候就能更方便地求新坐标了。

#### 本质意义

进一步地, 当 $A$ 是一个正交矩阵, 即做的是正交变换（以同向为例），那么有 
$$
\delta^{\prime}=A^{\prime} \delta=\left(\left|B_1\right|,\left|B_2\right|, \ldots,\left|B_n\right|\right)^T
$$
  于是有
$$
\alpha_i \cdot \delta=\left|B_i\right|(i=1,2, \ldots, n)
$$

考虑原标架是右手直角标架, 此时等号右边表示 $\delta$ 在第 $\mathrm{i}$个纬度上的分量为“高", 其他单位坐 标向量为“底"的几何体的“体积”。而“底"的面积为1, 所以这个“体积"就等于“高"。易知等号左边则表示 $\delta$ 在第 $\mathrm{i}$ 个纬度上的分量。

考虑原标架是任意标架，而且$ A$ 是任意可逆矩阵，那么可以类比地理解：一个向量在用一组新向量线性表出时在每个新向量的维度上的分量是以它为“高”、别的新坐标向量为“底”的几何体的体积比上新向量组构成的几何体的体积。

### 关于证明

1. 行列式的定义和应用：行列式是一个从数域的$n^2$维向量空间映射到数域自身的函数。在一个数域$F$上，我们可以定义一个行列式$\Delta$如下：

   $$\Delta : F^{n^2} \rightarrow F$$

   这个函数在$n$维线性空间$F^n$上是有效的。

2. 正交单位化：在一个数域$F$上，我们可以对$n$维线性空间$F^n$的任何基进行正交单位化。这可以把基转换为一个右手直角坐标系。

3. 克拉默法则的本质和应用：克拉默法则是一个几何直观的抽象，它在度量线性空间中有效。度量线性空间能表示诸如"面积"、"体积"这样的几何概念，而非度量空间不一定可以。

4. 线性方程组与线性空间的关系：线性方程组背后隐含了线性空间的结构，而二维和三维的几何可以帮助我们直观地理解数量关系（高维几何则需要依赖代数来理解）。

#### 结

**“克拉默法则的本质是将几何直观抽象到度量线性空间。”**



## reference

https://ccjou.wordpress.com/2009/11/10/%E5%85%8B%E6%8B%89%E7%91%AA%E5%85%AC%E5%BC%8F%E7%9A%84%E8%AD%89%E6%98%8E/

https://zhuanlan.zhihu.com/p/57944485

https://zhuanlan.zhihu.com/p/262988664

https://planetmath.org/proofofcramersrule