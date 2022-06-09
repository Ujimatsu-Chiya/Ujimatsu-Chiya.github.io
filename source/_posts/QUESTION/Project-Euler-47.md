---
title: Project Euler 47
tags:
  - Project Euler
mathjax: true
date: 2022-04-30 10:31:20
---

<escape><!-- more --></escape>

# Project Euler 47

## 题目

### Distinct primes factors

The first two consecutive numbers to have two distinct prime factors are:

$14 = 2 × 7\\ 15 = 3 × 5$

The first three consecutive numbers to have three distinct prime factors are:

$644 = 2^2 × 7 × 23\\ 645 = 3 × 5 × 43\\ 646 = 2 × 17 × 19.$

Find the first four consecutive integers to have four distinct prime factors each. What is the first of these numbers?

## 解决方案

本题没有比较好的估计上限的方式，故使用一个个合数从小到大枚举直接进行枚举的算法。

不过枚举过程中，有一点优化是：

假设现在正在判断$m,m+1,m+2,m+3$是所求解。那么，如果$m+x(0<x<4)$是不符合条件的数，那么可以直接忽略掉$m\sim m+x$之间的候选答案，直接判断后面4个数$m+x+1\sim m+x+4$。

这是因为只要在$m\sim m+x$之间选了一个答案，终究还是要对$m+x$进行判定，故直接跳过这一段中所有的数。

## 代码

```py
from tools import factorization

m = 2 * 3 * 5 * 7
ans = 0
while True:
    if len(factorization(m)) != 4:
        m += 1
    elif len(factorization(m + 1)) != 4:
        m += 2
    elif len(factorization(m + 2)) != 4:
        m += 3
    elif len(factorization(m + 3)) != 4:
        m += 4
    else:
        ans = m
        break
print(ans)

```
