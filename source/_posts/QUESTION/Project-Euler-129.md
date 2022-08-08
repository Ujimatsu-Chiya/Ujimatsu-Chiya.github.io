---
title: Project Euler 129
category:
  - Project Euler
tags:
mathjax: true
date: 2022-05-08 11:55:58
---

<escape><!-- more --></escape>

# Project Euler 129

## 题目

### Repunit divisibility

A number consisting entirely of ones is called a repunit. We shall define $R(k)$ to be a repunit of length $k$; for example, $R(6) = 111111$.

Given that $n$ is a positive integer and $\gcd(n, 10) = 1$, it can be shown that there always exists a value, $k$, for which $R(k)$ is divisible by $n$, and let $A(n)$ be the least such value of $k$; for example, $A(7) = 6$ and $A(41) = 5$.

The least value of $n$ for which $A(n)$ first exceeds ten is $17$.

Find the least value of $n$ for which $A(n)$ first exceeds one-million.

## 乘法群

设$\mathbb{Z}_{m}^*$为模数为$m$的乘法群。容易知道，乘法群是个循环群，而且其大小为$\varphi(m)$，其中$\varphi$为欧拉函数。

元素$a$在群$\mathbb{Z}_{m}^*$上的阶$\lambda_m(a)$：使得$a^k \equiv 1(\mod m)$的最小正整数$k$。

需要注意，一个元素的阶是群的大小的因数，也就是有$\forall a \in \mathbb{Z}_m^*,\lambda_m(a)|\varphi(m)$。

## 解决方案

可以通过用等比数列数列求和将$R(k)$表示出来：

$$R(k)=\dfrac{10^k-1}{9}$$

如果$n|R(k)$，即$9n|(10^k-1)$，那么有$10^k-1\equiv 0 (\mod 9n)$，也就是$10^k\equiv 1(\mod 9n)$。那么，$A(n)$就是求最小的**正整数**$k$，以使得$k$满足以下方程：

$$10^k\equiv 1(\mod 9n)$$

可以发现该问题为[离散对数问题](https://en.wikipedia.org/wiki/Discrete_logarithm)，主要常见的算法为[BSGS](https://en.wikipedia.org/wiki/Baby-step_giant-step)算法。不过，如果不限制$k$是正整数，BSGS算法将显而易见地给出$k=0$这个解。

根据$k$正整数的定义，可以发现，所求的$k$，其实是元素$10$在模乘法群$\mathbb{Z}_{9n}^*$中的阶$\lambda_{9n}(10)$，即$A(n)=\lambda_{9n}(10)$。

另外，容易观察到，$A(n)\leq n$。因此从$N=10^6$开始搜索。

本代码使用sympy库中的n_order(a,m)函数计算元素阶$\lambda_m(a)$的值。

## 代码

```py
from itertools import count

from sympy import n_order

N = 10 ** 6
for n in count(N | 1, 2):
    if n % 5 == 0:
        continue
    order = n_order(10, n * 9)
    if order >= N:
        ans = n
        break
print(ans)

```
