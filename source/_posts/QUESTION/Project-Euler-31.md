---
title: Project Euler 31
category:
  - Project Euler
tags:
  - 动态规划
mathjax: true
date: 2022-04-27 23:31:59
---

<escape><!-- more --></escape>

# Project Euler 31

## 题目

### Coin sums

In the United Kingdom the currency is made up of pound $(£)$ and pence $(p)$. There are eight coins in general circulation:

$$1p, 2p, 5p, 10p, 20p, 50p, £1 (100p), \text{and } £2 (200p).$$

It is possible to make $£2$ in the following way:

$$1×£1 + 1×50p + 2×20p + 1×5p + 1×2p + 3×1p$$

How many different ways can $£2$ be made using any number of coins?

## 解决方案

一个标准的完全背包问题（只不过并非是真正意义上的动态规划，这里是一个单纯的递推题目）。

记录状态$f(i,j)(1\leq i\leq n,0\leq j\leq m)$为：当前使用了前$i$种货币获得了$j$便士的方案数。

在这里，$n=8,m=200,a=[1,2,5,10,20,50,100,200]$.

那么，可以得到递推方程：

$$
f(i,j)=
\left \{\begin{aligned}
  &1  & & \text{if\quad} j=0 \\
  &0 & & \text{else if\quad} i=1 \land j<a[i] \\
  &f(i,j-a[i]) & & \text{else if\quad} i=1& \\
  &f(i-1,j) & & \text{else if\quad} j < a[i] \\
  &f(i-1,j) + f(i,j-a[i]) & & \text{else}
\end{aligned}\right.
$$

两种递推分别对应取真正取第$i$种货币和不取第$i$种货币。

## 代码

```Python
N = 200
ls = [1, 2, 5, 10, 20, 50, 100, 200]
f = [0 for x in range(N + 1)]
f[0] = 1
for x in ls:
    for i in range(x, N + 1):
        f[i] += f[i - x]
ans = f[N]
print(ans)
```
