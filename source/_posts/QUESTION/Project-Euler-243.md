---
title: Project Euler 243
category:
  - Project Euler
tags:
mathjax: true
date: 2022-06-18 21:59:02
---

<escape><!-- more --></escape>

# Project Euler 243

## 题目

### Resilience

A positive fraction whose numerator is less than its denominator is called a proper fraction.

For any denominator, $d$, there will be $d−1$ proper fractions; for example, with $d=12$:

$\dfrac{1}{12},\dfrac{2}{12},\dfrac{3}{12},\dfrac{4}{12},\dfrac{5}{12},\dfrac{6}{12},\dfrac{7}{12},\dfrac{8}{12},\dfrac{9}{12},\dfrac{10}{12},\dfrac{11}{12}$

We shall call a fraction that cannot be cancelled down a *resilient fraction*.

Furthermore we shall define the *resilience* of a denominator, $R(d)$, to be the ratio of its proper fractions that are resilient; for example, $R(12) = \dfrac{4}{11}$ .

In fact, $d=12$ is the smallest denominator having a resilience $R(d) < \dfrac{4}{10}$.

Find the smallest denominator $d$, having a resilience $R(d) < \dfrac{15499}{94744}$ .

## 解决方案

令$r=\dfrac{15499}{94799}$

根据欧拉函数$\varphi$的定义，可以知道$R(d)=\dfrac{\varphi(d)}{d-1}$.

如果一个数$n$中质因数越来越多，那么$\dfrac{\varphi(n)}{n-1}$就会显著降低，因为随着$n$的增大这个比值会无限趋近于$\dfrac{\varphi(n)}{n}$。如果一个数$n$，它的质因数的幂指数越大，那么对答案的贡献将会越低。

并且，如果这些质因数越小，$\dfrac{\varphi(n)}{n-1}$下降的越明显。基于这种贪心的思想，假设$n=\prod_{i=1}^m pr[i]$，其中$pr$是一个从小到大的质数列表。

从小到大枚举$m$，计算出$n$的值。如果发现$\dfrac{\varphi(n)}{n-1}< r$，那么可以不必再找下去，$n$将是一个候选的答案。如果$\dfrac{\varphi(n)}{n-1}\ge r$，但是$\dfrac{\varphi(n)}{n}< r$ ，那么可以考虑寻找$n$的最小的倍数$k$，使得$\dfrac{\varphi(k)}{k}< r$，这些$k$也是一个候选答案。

这些候选答案的最小值就是最终答案，枚举速度很快。

## 代码

```py
from sympy import nextprime
from fractions import Fraction
from math import ceil

U, D = 15499, 94744
f = Fraction(U, D)
p = 2
ans = 10 ** 100
phi, n = 1, 1
while True:
    n *= p
    phi *= p - 1
    if Fraction(phi, n - 1) < f:
        ans = min(ans, n)
        break
    elif Fraction(phi, n) < f:
        # 计算出，k至少是n的c倍时，才会有phi(k)/(k-1)<r。
        x = -f / (phi - n * f)
        c = ceil(x)
        if c == x:
            c += 1
        ans = min(ans, c * n)
    p = nextprime(p)
print(ans)
```
