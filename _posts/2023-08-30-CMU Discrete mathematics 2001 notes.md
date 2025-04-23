---
layout: post
title:  "Discrete Mathematics"
date: 2023-08-30
---

虎头蛇尾…

# 离散数学 CMU 2001 notes

# Lec1 

## intro

…

## Set

1. 首先定义空集的概念  $\empty$ **Definition**: the only set include no elements.

2. 交并补的概念    <font color='red'>补充</font> 

   



## The Sum Principle<font color='red'>补充</font>



## Proof of Ramsey’s Theorem





你想证明的这个等式可以通过组合数的性质和帕斯卡三角形来解释和证明。以下是证明的一种方式：

首先，我们知道组合数 $\binom{n}{m}$ 表示从 $n$ 个元素中选择 $m$ 个元素的组合数。这可以表示为：

$$\binom{n}{m} = \frac{n!}{m!(n-m)!}$$

同样，$\binom{n}{m+1}$ 表示从 $n$ 个元素中选择 $m+1$ 个元素的组合数：

$$\binom{n}{m+1} = \frac{n!}{(m+1)!(n-m-1)!}$$

然后，我们来看左边的等式：

$$\binom{n}{m} + \binom{n}{m+1}$$

将上述两个组合数的表达式代入，得到：

$$\frac{n!}{m!(n-m)!} + \frac{n!}{(m+1)!(n-m-1)!}$$

现在，我们的目标是将这个式子变形成 $\binom{n+1}{m+1}$ 的形式。我们注意到，$\binom{n+1}{m+1}$ 也是从 $n+1$ 个元素中选择 $m+1$ 个元素的组合数：

$$\binom{n+1}{m+1} = \frac{(n+1)!}{(m+1)!(n-m)!}$$

我们希望将左边的式子变形成 $\binom{n+1}{m+1}$ 的形式。为此，我们可以考虑如何将两个分数相加，使得分母部分与 $\binom{n+1}{m+1}$ 相同。我们观察到：

$$\frac{n!}{m!(n-m)!} + \frac{n!}{(m+1)!(n-m-1)!} = \frac{(n+1)!}{(m+1)!(n-m)!}$$

上述等式成立是因为分子部分相等。这就完成了证明。

因此，我们证明了：

$$\binom{n}{m} + \binom{n}{m+1} = \binom{n+1}{m+1}$$

这个等式在组合数学中被称为 Pascal's Rule（帕斯卡规则），它在帕斯卡三角形中有重要的几何解释。

## 下面笔记使用北理莫斯科的lec notes

## Fri. 18th





## 3.2 集合的概念

**<font color='green'>集合 </font>** 

**定义** 我们指元素的组合。

**数学描述**<font color='red'>latex打不出空格</font>{} 
$$
A={a:a满足specific的性质}
$$
**<font color='green'>两个集合的差集 </font>** 

**定义**





### 3.2.2 关系

#### 二元关系

<font color='red'>什么是二元关系，没有被定义</font> 

<font color='blue'>我觉得是两个未知数的关系就是2元关系</font> 



<font color='red'>问:满足函数关系的本事是不是要满足映射关系，映射关系set A 到set  B，从一个A的element出发，只对应一个set B中的b，但是没有说是满射(满射)的英文是什么onto？</font> 

**onto** 是set B 中的b elements at least 对应一个 set A中的a



## 8 20th 计数

例 3.16. 定义 $[n]^{(r)}=\{T \subseteq\{1,2, \ldots, n\}:|T|=r\}$. 设 $\mathcal{A} \subseteq[n]^{(r)}$. 设 $s>r$ 。定义
$$
\mathcal{B}=\left\{B \in[n]^{(s)}: \exists A \in \mathcal{A}, \text { s.t. } A \subseteq B\right\} .
$$
$|\mathcal{B}|$ 有多大呢（当然 $|\mathcal{B}|$ 依赖于 $|\mathcal{A}|)$ ?
解答. 上界：根据定义 $\mathcal{B} \subseteq[n]^{(s)}$ ，所以 $|\mathcal{B}| \leq\left|[n]^{(s)}\right|=\left(\begin{array}{l}n \\ s\end{array}\right)$.
下界：考虑如下集合
$$
M=\{(A, B) \in \mathcal{A} \times \mathcal{B}: A \subseteq B\} .
$$
分别采用 $\mathcal{A}$ 和 $\mathcal{B}$ 的观点来计算 $|M|$ 。
- 从 $\mathcal{A}$ 的观点：对每个 $A \in \mathcal{A}, A$ 包含在 $\left(\begin{array}{l}n-r \\ s-r\end{array}\right)$ 个不同的 $B$ 中。因此, $|M|=|\mathcal{A}|\left(\begin{array}{l}n-r \\ s-r\end{array}\right)$.
- 从 $\mathcal{B}$ 的观点：对每个 $B \in \mathcal{B}, B$ 最多包含 $\left(\begin{array}{l}s \\ r\end{array}\right)$ 个不同的 $A$ 。因此, $|M| \leq|\mathcal{B}|\left(\begin{array}{l}s \\ r\end{array}\right)$.



### 解释

<font color='red'>$[n]^{(r)}=\{T \subseteq\{1,2, \ldots, n\}:|T|=r\}$</font> 

对这个定义的明晰

$[ ]$ and $()$ 都是对set的描述，其中集合中元素的个数的表示方法是$|A|$ ，比如$|\mathcal{P}(A)|=2^{|A|}$ 

$\{T \subseteq\{1,2, \ldots, n\}\}$

则表示$T$ 被这个set包含，T中可能有1-n之间的元素，

$|T|=r$ 

说明T的size就是r

$[n]^{(r)}$ 

说明有r组n这个set要配对，T中的元素分别输出到n值



$[n]^{(r)}$ 表示从集合 ${1, 2, \ldots, n}$ 中选取$r$个元素的所有可能集合。而不是 "有r组n这个set要配对，T中的元素分别输出到n值"。

$[n]^{(r)}$ 表示的是从集合 ${1, 2, \ldots, n}$ 中选取$r$个元素的所有可能集合，而不是将元素与n进行配对。



## 康尔托对角线证法

主要的构造方法是在[0,1]中，使用小数表示一个自然数，或者说使用一个双射来连接关系的情况下，特使得$x_{ij}(j=i)$ 的位置设置一个不同数，使用这个方式，当一个数字的每个数上的位置，不可以被对角线上对应位置的数字表示的时候，就说明他

## 图 Tue.

### 定义4.1

**欧拉通路**：经过图中的每一条边一次且仅一次。

**欧拉回路**：经过图中的每一条边一次且仅一次，且回到出发点。

### 定义4.2

设 v 是图中的某个顶点，与 v 连接的边的数目叫做 v 的度数，记作 d(v)。

###命题 4.3

对任意的图 G，如果图 G 中存在一条欧拉**通路**，则**最多**只有**两个**点的度数是奇数。

### 命题 4.4

对任意的图 G，如果图 G 中存在一条欧拉**回路**，则**每个**点的度数都是**偶数**

*命题4.4和4.3 只可以判断在本身存在时，这里的检测方法就是说，*

### 定义 4.5

一个（无向，即边没有方向）图 $G$  由点和边组成，点的集合通常用$V$   表示，边的集合用 $E$  表示。图 $G$ 一般写作
$$
G = (V, E)
$$
**点的相邻** 两个**点**有边

**边的相邻** 两个边之间有点

**点的度数** 点发散或者接收的条数

**简单图** 两点之间最多一条边（不会不复杂，但是会没有来回

<font color='red'>**通路** 从一点到另一点由边连接的序列（点和边均允许重复）</font> 

<font color='red'>**路径** **点**<font color='green'>不重复</font>的通路</font> 

<font color='red'>**回路** 起点和终点相同的通路</font> **(到底是一个成环的路还是？首尾链接的路可以)**

**连通图** 任意两点之间均有通路连接



**子图** 由图的某些点和这些点上某些边组成的图

导出子图：由图的某些点和这些点上所有的边组成的图/*感觉没什么用，就是选了一些线和点呗*

连通分支：

### 定理4.7

对任意的连通图 G，

* 图 G 中存在一条欧拉通路，**当且仅**当要么每个点的度数都是偶数，要么恰有两点的度数是奇数。
*  图 G 中存在一条欧拉回路，**当且仅当**每个点的度数都是偶数。

***充分必要？***

### 定理4.8 &4.9握手定理和其的推论

有点问题

使用对称理论证明

## 树与环 Aug. 25th

定义



## Aug. 26th 图的同构

**定义**

对有些问题而言，我们只关心边的相互关系，并不对顶点做过多区分，数学上我们考虑一个新的概念，叫做同构。

满足双射，在两个图$G=(V,E)$ 和$H=(V',E')$中，





三个算法

### 1. 贪心算法 最小生成树 Kruskal 算法

具向的理解是首先把最短到最长的权重的line升序排列取出，再使用这些line上的权重值进行连接，在连接时观察是否连结成环，如果成环，则取消

### 2. 信息熵算法



### 3. Dijkstra 算法







