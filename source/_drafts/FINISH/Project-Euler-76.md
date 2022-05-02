---
title: Project Euler 76
tags:
  - Project Euler
  - 动态规划
mathjax: true
---
<escape><!-- more --></escape>

# Project Euler 76

## 题目

### Counting summations

It is possible to write five as a sum in exactly six different ways:

$4 + 1$
$3 + 2$
$3 + 1 + 1$
$2 + 2 + 1$
$2 + 1 + 1 + 1$
$1 + 1 + 1 + 1 + 1$

How many different ways can one hundred be written as a sum of at least two positive integers?

## 解决方案

本体是一个明显的动态规划。

令$n=100$，记录状态$f(i,j)(1\leq i\leq n,0\leq j\leq n)$为：当前已经使用了前$1\sim i$中所有数，可以凑得和为$j$的方案数。可写出如下状态转移方程：

$$
f(i,j)=
\left \{\begin{aligned}
  &1  & & \mathrm{if\quad} j=0 |i=1 \\
  &f(i-1,j)  & & \mathrm{else if\quad} j<i \\
  &f(i-1,j)+f(i,j-i) & & \mathrm{else}
\end{aligned}\right.
$$

对于最后一题式子，有两种转移方式：

1. 不使用第$i$个数，直接把使用前$i-1$个数的情况记录下来。
2. 使用第$i$个数，无论之前如何，直接把$f(i,j-i)$中的所有方案都添加一个$i$，就变成了现在的方案。

## 代码

```py
N = 100
f = [0 for _ in range(N + 1)]
f[0] = 1
for i in range(1, N + 1):
    for j in range(i, N + 1):
        f[j] += f[j - i]
print(f[N] - 1)

```
