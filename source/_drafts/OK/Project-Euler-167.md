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

这篇[文章](http://projecteuclid.org/download/pdf_1/euclid.em/1048709116)提到，形如$U(2,2n+1),n\ge 2$的乌拉姆序列，有且仅有两个项是偶数，分别为$2$和$4n+4$。


这个[页面](https://mathworld.wolfram.com/UlamSequence.html)提到：如果乌拉姆序列中偶数的个数是有限的，那么它的差分序列是周期的。


## 代码


