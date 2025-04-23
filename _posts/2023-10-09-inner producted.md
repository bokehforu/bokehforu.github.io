---
layout: post
title:  "Inner producted 一些问题"
date: 2023-10-09
---

A record of some simple ideas.



##  vector inner product

**向量的内积**

- 内积的定义:
   - 设A和B为两个向量,它们的内积定义为A在B上的投影长度,用公式表示为<A,B> = |A||B|cosθ,其中θ是两向量之间的角度。

- 内积的几何意义:内积反映了两个向量间的相似程度,当两个向量方向相同时内积最大;when两向量垂直时内积为0。

- 如何计算两个向量的内积:设两个n维向量为A=(a1,a2,...,an),B=(b1,b2,...,bn),则两向量的内积为<A,B> = a1b1 + a2b2 + ... + anbn,即对应元素相乘并求和。

- 内积为何等于零:当两个向量垂直时,cosθ=0,从内积公式可知此时<A,B>=0。也就是说,内积等于零表示两个向量互相垂直。

## matrix inner product

- 矩阵内积的定义:对于两个矩阵A和B,它们的内积定义为:<A,B> = tr(A^TB),即矩阵A与B转置矩阵的乘积的**迹**,什么是迹，就是从左到右的对角线。
- 矩阵内积与迹的关系:矩阵内积用矩阵迹来表达,迹反映了矩阵的特征,内积刻画了两个矩阵间的相关性。
- 如何计算两个矩阵的内积:对两个矩阵A和B,计算A^TB,然后求出其迹(对角元素之和)即可。
- 矩阵内积的性质:
   - 对称性 <A,B> = <B,A> 
   - 双线性形式 
   - 范数不等式$|<A,B>| <= ||A|| · ||B||$ <font color='red'>这啥</font>

- matrix的变换。



## f(x) and g(x) inner product

- 函数内积的定义:对于区间[a,b]上的连续函数f(x)和g(x),它们的内积定义为$$\langle f, g\rangle=\int_a^b f(x) g(x) d x$$

- 如何利用积分计算函数内积:将函数相乘后对区间[a,b]积分,即可计算内积。

- 函数内积的双线性形式:满足α<f,g> = <αf,g> = <f,αg> 

- 函数内积与区间长度的关系:内积与区间长度成正比,因此也会normalize由 $\int ab$  改为 $\int \frac{ab}{L}$。

- 函数内积的应用:反映函数间相关性,应用于信号处理、模式识别等领域。

$$\langle f, g\rangle=\int_a^b f(x) g(x) d x$$

or another choice

$$\langle f, g\rangle=\frac{1}{b-a} \int_a^b f(x) g(x) d x$$

第一种表示法:

$$\langle f, g\rangle=\int_a^b f(x) g(x) dx$$

直接对函数的乘积在区间[a,b]上进行积分即可得到内积。

第二种表示法:

$$\langle f, g\rangle=\frac{1}{b-a}\int_a^b f(x) g(x) dx$$

在积分中额外引入了比例系数$\frac{1}{b-a}$,目的是归一化区间[a,b]的长度,使得内积不直接依赖于区间长度。



## 应用：傅立叶级数
