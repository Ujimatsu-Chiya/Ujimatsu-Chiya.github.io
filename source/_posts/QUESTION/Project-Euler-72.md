---
title: Project Euler 72
tags:
  - Project Euler
mathjax: true
date: 2022-05-02 16:36:18
---

<escape><!-- more --></escape>

# Project Euler 72

## 题目

### Counting fractions

Consider the fraction, $\dfrac{n}{d}$, where n and d are positive integers. If $n<d$ and $\gcd(n,d)=1$, it is called a reduced proper fraction.
If we list the set of reduced proper fractions for $d \leq 8$ in ascending order of size, we get:

$$\dfrac{1}{8},\dfrac{1}{7},\dfrac{1}{6},\dfrac{1}{5},\dfrac{1}{4},\dfrac{2}{7},\dfrac{1}{3},\dfrac{3}{8},\dfrac{2}{5},\dfrac{3}{7},\dfrac{1}{2},\dfrac{4}{7},\dfrac{3}{5},\dfrac{5}{8},\dfrac{2}{3},\dfrac{5}{7},\dfrac{3}{4},\dfrac{4}{5},\dfrac{5}{6},\dfrac{6}{7},\dfrac{7}{8}$$

It can be seen that there are $21$ elements in this set.

How many elements would be contained in the set of reduced proper fractions for $d \leq 1,000,000$?

## 解决方案

根据题意，第$m$个[Farey 序列](https://en.wikipedia.org/wiki/Farey_sequence)$F_m$的所有元素可以由该集合定义：$\{\dfrac{n}{d} | \gcd(n,d)=1,1\le n<d \le m\}$.

通过分子分母互质的性质，联系到欧拉函数$\varphi$的定义，可以得出本题答案：

$$\sum_{i=1}^m \varphi(i)-1$$

## 代码

```py
N = 1000000
phi = [i for i in range(N + 1)]
for i in range(2, N + 1):
    if i == phi[i]:
        for j in range(i, N + 1, i):
            phi[j] //= i
            phi[j] *= i - 1
print(sum(phi) - 1)

```
