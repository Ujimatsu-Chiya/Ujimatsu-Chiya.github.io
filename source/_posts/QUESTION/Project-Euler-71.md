---
title: Project Euler 71
category:
  - Project Euler
tags:
mathjax: true
date: 2022-05-02 16:36:14
---

<escape><!-- more --></escape>

# Project Euler 71

## 题目

### Ordered fractions

Consider the fraction, $\dfrac{n}{d}$, where n and d are positive integers. If $n<d$ and $\gcd(n,d)=1$, it is called a reduced proper fraction.
If we list the set of reduced proper fractions for $d \leq 8$ in ascending order of size, we get:

$$\dfrac{1}{8},\dfrac{1}{7},\dfrac{1}{6},\dfrac{1}{5},\dfrac{1}{4},\dfrac{2}{7},\dfrac{1}{3},\dfrac{3}{8},\mathbf{\dfrac{2}{5}},\dfrac{3}{7},\dfrac{1}{2},\dfrac{4}{7},\dfrac{3}{5},\dfrac{5}{8},\dfrac{2}{3},\dfrac{5}{7},\dfrac{3}{4},\dfrac{4}{5},\dfrac{5}{6},\dfrac{6}{7},\dfrac{7}{8}$$

It can be seen that $\dfrac{2}{5}$ is the fraction immediately to the left of $\dfrac{3}{7}$.
By listing the set of reduced proper fractions for $d \leq 1,000,000$ in ascending order of size, find the numerator of the fraction immediately to the left of $\dfrac{3}{7}$.

## 解决方案

本题所描述的序列为[Farey 序列](https://en.wikipedia.org/wiki/Farey_sequence)。该序列有如下性质：

对于任意的Farey 序列$F_n$，其中任意连续的三个分数序列$\dfrac{x_1}{y_1},\dfrac{x_2}{y_2},\dfrac{x_3}{y_3}$，满足$\dfrac{x_2}{y_2}=\dfrac{x_1+x_3}{y_1+y_3}$。

本题目前比$\dfrac{3}{7}$小的最大分数为$\dfrac{2}{5}$，在中间插入一个新值$\dfrac{3+2}{7+5}=\dfrac{5}{12}$后，可以发现这个新值比$\dfrac{2}{5}$更大，但同时还是比$\dfrac{3}{7}$小。在$\dfrac{5}{12}$和$\dfrac{3}{7}$中间继续插入后，得到$\dfrac{8}{19}...$

以此类推，每插入一个新的数，分子增长$3$，分母增长了$7$，新插入值的序列可以用$\dfrac{2+3k}{5+7k}$来表示。

因此，所求分数的值满足最大的$k$使得$5+7k\leq 10^6$。

## 代码

```py
N = 10 ** 6
ru, rd = 3, 7
lu, ld = 2, 5

k = (N - ld) // rd
ans = lu + ru * k
print(ans)

```
