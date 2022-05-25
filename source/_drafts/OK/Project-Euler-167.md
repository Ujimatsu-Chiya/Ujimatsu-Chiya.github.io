---
title: Project Euler 167
tags:
  - Project Euler
  - 论文
mathjax: true
---
<escape><!-- more --></escape>
    
    

# Project Euler 167
## 题目
### Investigating Ulam sequences
For two positive integers $a$ and $b$, the Ulam sequence $U(a,b)$ is defined by $U(a,b)_1 = a$, $U(a,b)_2 = b$ and for $k > 2,U(a,b)_k$ is the smallest integer greater than $U(a,b)_{(k-1)}$ which can be written in exactly one way as the sum of two distinct previous members of U(a,b).

For example, the sequence $U(1,2)$ begins with

$1, 2, 3 = 1 + 2, 4 = 1 + 3, 6 = 2 + 4, 8 = 2 + 6, 11 = 3 + 8;$

$5$ does not belong to it because $5 = 1 + 4 = 2 + 3$ has two representations as the sum of two previous members, likewise $7 = 1 + 6 = 3 + 4$.

Find $\sum U(2,2n+1)_k$ for $2 \leq n \leq 10$, where k = $10^{11}$.


## 解决方案

1. 这篇[文章](http://projecteuclid.org/download/pdf_1/euclid.em/1048709116)提到，形如$U(2,2n+1),n\ge 2$的乌拉姆序列，有且仅有两个项是偶数，分别为第$1$项的$2$和第$n+4$项的$4n+4$。


2. 这个[页面](https://mathworld.wolfram.com/UlamSequence.html)提到：如果乌拉姆序列中偶数的个数是有限的，那么它的差分序列是周期的。

第一个问题：如何高效计算序列$U(2,2n+1)$？

不难看出，第$2$项和第$n+3$项之间的所有的奇数项是以$2n+1$为首项，$2$为公差的等差数列。

根据乌拉姆序列的定义，第$i$项$U(2,2n+1)_i$一定由序列之前的某两个项相加而成。又由于第$n+5$项及以后的所有项都是奇数，那么这些项一定是由一个奇数和一个偶数相加得出，这个偶数要么是$2$，要么是$4n+4$。因此这将帮助我们以线性阶的时间复杂度计算序列$U(2,2n+1)$：计算一个奇数$x$是否在$U(2,2n+1)$，只需要判断$x-2$和$x-(4n+4)$是否**有且仅有其中一个**在$U(2,2n+1)$中。



## 代码


