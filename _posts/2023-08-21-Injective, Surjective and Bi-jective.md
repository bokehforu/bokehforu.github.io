---
layout: post
title:  "Injective, Surjective and bi-jective"
date: 2023-08-21
---

A small concept in discrete mathematics

# 函数的类别 Injective, Surjective and bi-jective

## Functions, Domain, Codomain,Range

**Function（函数）**

函数是一种关系，在给定定义域的情况下，将定义域中的每个元素**映射**到唯一的值域中的元素。函数通常用 f(x) 或 g(y) 等符号表示，其中 x 和 y 是定义域和值域中的元素。函数描述了输入和输出之间的映射关系。

**Domain（定义域）**

The set of input values

定义域是函数的所有可能输入值的集合。它是函数可以接受的输入范围。例如，对于函数 f(x) = x^2，定义域可以是实数集合 R，因为任何实数都可以作为该函数的输入。

**Codomain（值域）** 

The set of possible output values <font color='red'>那我感觉codomian就一直是$\R$</font> <font color='blue'>我有点不太理解这个codmain这个set是如何产生的，一个</font> 

值域是函数中所有可能的输出值的集合。它是函数可以产生的所有可能结果的范围。与定义域不同，值域不一定是函数实际映射到的值的集合，而是函数可能生成的所有结果的集合。例如，对于函数 f(x) = x^2，值域可以是非负实数集合 R≥0，因为平方函数的结果始终为非负实数。

**Range（值域*）**

The set of actual output values

Range是函数实际映射到的值的集合。它是函数在给定定义域上生成的所有实际输出值的集合。通常，值域是通过确定函数的所有可能输出值并排除任何不可达的值来确定的。例如，对于函数 f(x) = x^2，如果定义域为实数集合 R，那么值域将是非负实数集合 R≥0，因为平方函数的结果始终为非负实数。 

## Injective, Surjective and bi-jective定义和简明解释

Definition

来源： https://www.math.fsu.edu/~pkirby/mad2104/SlideShow/s4_2.pdf

Given $f: A \rightarrow B$

1. $f$ is **one-to-one** (short hand is $1-1$ ) or **injective** if preimages(预先映射) are unique. In this case, $(a \neq b) \rightarrow(f(a) \neq f(b))$. <font color='red'>一个a只匹配一个在set B中的b</font> 

2. $f$ is **onto** or **surjective** if every $y \in B$ has a preimage. In this case, the range of $f$ is equal to the codomain.<font color='red'>我感觉codomian和range的关系没搞明白</font> 

3. $f$ is **bijective** if it is surjective and injective (one-to-one and onto).



来源：**YouTube视频**

* one to one / injective
   * For
      every input there is unique output. All the elements in the domain
      have to be used, but **all** elements in the co-domain **need not be used**.就是在input的元素中，映射出去，co-domain中要留有剩余。
   * 
* onto / Surjective 
   * (Range
      = co-domain)
      Every element in the co-domain is the image of **at least** one element in
      the domain. 
   * 或者说range要=co-domain 
* bijective 
   * These functions are one-one functions but **every** element in the co-domain
      is used.

### 我的理解

对于函数，我们考虑到A这个set和B这个set中存在的一些元素，这是背景信息要求。那么，当A的元素出发对应到了B中的元素，这就是满足函数的关系。在这个基础上有两个方向。<font color='red'>第一个方向是one to one，这个对满足function的关系的要求基础之上，额外要求对于set A中的元素应该全部射出，set B可以留有空白的元素。</font> 而另外一个方向，则是指明了在set B中，B中的元素全部至少被A中的一个元素被射中，甚至可以被A中的多个元素射中。而bijective 就是这两个路径的叠加，就是set A中的元素被全部射出，而set B中的元素全部被set A中的元素对应



<font color='red'>上面的理解感觉是错的</font> ，红色部分one to one的理解错了



### 新的理解

https://www.youtube.com/watch?v=MY4-5mXfWzo&ab_channel=Areallnamesgone

视频中显示，函数的定义是set A中的元素都是单个箭头出发，而不是从a1出发有两个箭头，满足了这个关系就是**函数**，我觉得这个好理解，因为满足了线性关系后，set A中的元素对应了两个set B中的元素(比如f(1)=2但是f(1)又可以=34)，这非常奇怪了，线性关系就被破坏了。继续到**one to one**，可以进行字面意思的理解，one to one就是在set A到 set B的映射关系中，一个在set A(domain)中的元素只可以唯一对应set B中的元素，比如(set A{a_1,a_2,a_3,a_4}和set B{b_1,b_2,b_3,b_4,b_5}这里的元素，假设他们下标匹配对应，a_1配备b_1…最后留下b_5是空的，没有被A中的元素中对应的，这样也是可以的。因为这个case满足了我们对于set A中的元素都要可以对应set B中的这种情况)。继续**onto**，这个要求是set B中的元素at least 都要被A中出发的元素射中，就是说set B没有空的元素，但是一个在set B中的元素可以被很多从set A的元素出发的箭头(关系)对应。最后**bijective**，满足了set A中的单一输出箭头(函数，映射关系)都有一个在set B中对应的元素(one to one)，同时set B中的元素都接受到set A的元素中出发的箭头(onto),这两个路径的分别满足，让set A和set B中的元素得到了全部的匹配和各自唯一的匹配。

##   Function关系的演变



![function-mapping](https://www.mathsisfun.com/sets/images/function-mapping.svg)



https://www.youtube.com/watch?v=ojHAAqgW1_M&ab_channel=TheMathSorcerer

