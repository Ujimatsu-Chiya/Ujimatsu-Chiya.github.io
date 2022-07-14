---
title: Project Euler 686
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>

# Project Euler 686

## 题目

### Powers of Two

$2^7=128$ is the first power of two whose leading digits are "$12$".

The next power of two whose leading digits are "$12$" is $2^{80}$.

Define $p(L, n)$ to be the $n\text{th}$-smallest value of $j$ such that the base $10$ representation of $2^j$ begins with the digits of $L$.

So $p(12, 1) = 7$ and $p(12, 2) = 80$.

You are also given that $p(123, 45) = 12710$.

Find $p(123, 678910)$.

## 解决方案

将$2^k$对$10$进行取对数，那么得到$k\log_{10} 2$。如果$2^k$是以$123$为开头，那么$k\log_{10}2$的小数部分$d=k\log _{10}2-\lfloor k\log_{10}2\rfloor$满足$\log_{10}1.23\le d<\log_{10} 1.24$。因此，最朴素的一种做法是从小到大枚举$k$，观察$k\log_{10}2$的小数部分是否落在那个区间上即可。这个区间写成小数部分是：

$[0.08990511143939793,0.09342168516223506)$

不过，朴素枚举区间的效率似乎比较慢。暴力枚举出前几项后，发现相邻的两项差值总在集合$\{196, 289, 485\}$中。




## 代码
