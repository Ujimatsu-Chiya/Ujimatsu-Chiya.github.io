---
title: Project Euler 15
category:
  - Project Euler
tags:
mathjax: true
date: 2022-04-27 09:55:34
---

<escape><!-- more --></escape>

# Project Euler 15

## 题目

### Lattice paths

Starting in the top left corner of a $2×2$ grid, and only being able to move to the right and down, there are exactly $6$ routes to the bottom right corner.

![](../images/p015.png)

How many such routes are there through a $20\times20$ grid?

## 解决方案

假设这个方格一共有$n\times m$格，在这里，$n=m=20$.

假设往下走一步，得到一个字母D，往右走一步，得到一个字母R。那么一共可以得到$n$个D和$m$个R。

但是，走的过程是可以随时变化的，这也对应了每个D和R的序列顺序不一样（但仍然保持有$n$个D和$m$个R）。

问题就转化成了组合数，因此，答案是$C_{n+m}^m$

这里使用了sympy的函数binomial求组合数，之后将封装在tools自定义工具类中，以C(n,m)的方式调用。

## 代码

```py
from sympy import binomial

n = m = 20
ans = binomial(n + m, m)
print(ans)
```
