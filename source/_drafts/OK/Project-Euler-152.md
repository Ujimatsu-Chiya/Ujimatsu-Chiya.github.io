---
title: Project Euler 152
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 152
## 题目
### Writing 1/2 as a sum of inverse squares


There are several ways to write the number $\dfrac{1}{2}$ as a sum of inverse squares using *distinct* integers.

For instance, the numbers $\{2,3,4,5,7,12,15,20,28,35\}$ can be used:
$$\dfrac{1}{2} = \dfrac{1}{2^2} + \dfrac{1}{3^2} + \dfrac{1}{4^2} + \dfrac{1}{5^2}+
\dfrac{1}{7^2} + \dfrac{1}{12^2} + \dfrac{1}{15^2} + \dfrac{1}{20^2} +
\dfrac{1}{28^2} + \dfrac{1}{35^2}$$

In fact, only using integers between $2$ and $45$ inclusive, there are exactly three ways to do it, the remaining two being: $\{2,3,4,6,7,9,10,20,28,35,36,45\}$ and $\{2,3,4,6,7,9,12,15,28,30,35,36,45\}$.

How many ways are there to write the number $\dfrac{1}{2}$ as a sum of inverse squares using distinct integers between $2$ and $80$ inclusive?


## 解决方案

为减少枚举量，进行以下排除：

1. $\dfrac{1}{2^2}$一定在答案集合中，因为$\sum_{i=3}^{80} \dfrac{1}{i^2}<\dfrac{1}{2}$

2. 考虑所有质数$p$，令$q=p^r$，其中$r$是使$p^r$不超过$N=80$的最大值。

在这种情况下，考虑所有满足$kq\le N$的分数$\dfrac{1}{q^2},\dfrac{1}{(2q)^2},\dots,\dfrac{1}{(kq)^2}$

考虑计算$\dfrac{1}{(i_1q)^2}+\dfrac{1}{(i_2q)^2}+\dots+\dfrac{1}{(i_mq)^2}$，其中$i_j<p$，不同的$i_j$之间两两不同。

那么有$\dfrac{1}{q^2}(\dfrac{1}{i_1^2}+\dfrac{1}{i_2^2}+\dots+\dfrac{1}{i_m^2})$

如果在计算分数和的过程中，分母混进了一个不属于$2$的质数$p$，那么在求和的过程中必须消除。因此$\sum_{j=1}^m i_j^{-2}$在模$q^2$上与$0$同余。

- 对于大于$\dfrac{N}{2}$的质数而言，集合中只有元素$1$，不可能存在一个非空集合使得


## 代码


