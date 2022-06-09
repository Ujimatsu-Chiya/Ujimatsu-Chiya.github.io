---
title: Project Euler 77
tags:
  - Project Euler
  - 动态规划
mathjax: true
date: 2022-05-02 16:36:37
---

<escape><!-- more --></escape>

# Project Euler 77

## 题目

### Prime summations

It is possible to write ten as the sum of primes in exactly five different ways:

$7 + 3$<br>
$5 + 5$<br>
$5 + 3 + 2$<br>
$3 + 3 + 2 + 2$<br>
$2 + 2 + 2 + 2 + 2$

What is the first value which can be written as the sum of primes in over five thousand different ways?

## 解决方案

本体是一个明显的动态规划，与76题的做法基本上一样。

从小到大枚举$n$值，直到方案数超过$5000$。

令$m$为$n$以内的质数个数，数组$p$为这$m$个从小到大排序的质数。
记录状态$f(i,j)(1\leq i\leq m,0\leq j\leq n)$为：当前已经使用了前$i$种质数，可以凑得和为$j$的方案数。可写出如下状态转移方程：

$$
f(i,j)=
\left \{\begin{aligned}
  &1  & & \mathrm{if\quad} j=0 |(i=1 \&j\%p[1]=0)  \\
  &0  & & \mathrm{else if\quad} i=1 \\
  &f(i-1,j)  & & \mathrm{else if\quad} j<p[i] \\
  &f(i-1,j)+f(i,j-p[i]) & & \mathrm{else}
\end{aligned}\right.
$$

对于最后一题式子，有两种转移方式：

1. 不使用第$i$个质数，直接把使用前$i-1$个数的情况记录下来。
2. 使用第$i$个质数数，无论之前如何，直接把$f(i,j-p[i])$中的所有方案都添加一个$p[i]$，就变成了现在的方案。

## 代码

```py
from itertools import count
from tools import is_prime

N = 5000
pr = []
for n in count(2, 1):
    if is_prime(n):
        pr.append(n)
    f = [0 for _ in range(n + 1)]
    f[0] = 1
    for x in pr:
        for j in range(x, n + 1):
            f[j] += f[j - x]
    if f[n] >= N:
        ans = n
        break
print(ans)

```
