---
title: Project Euler 694
category:
  - Project Euler
tags:
mathjax: true
date: 2022-07-17 23:11:32
---

<escape><!-- more --></escape>

# Project Euler 694

## 题目

### Cube-full Divisors

A positive integer $n$ is considered *cube-full*, if for every prime $p$ that divides $n$, so does $p^3$. Note that $1$ is considered cube-full.

Let $s(n)$ be the function that counts the number of cube-full divisors of $n$. For example, $1$, $8$ and $16$ are the three cube-full divisors of $16$. Therefore, $s(16)=3$.

Let $S(n)$ represent the summatory function of $s(n)$, that is $S(n)=\displaystyle\sum_{i=1}^n s(i)$.

You are given $S(16) =  19$, $S(100) = 126$ and $S(10000) = 13344$.

Find $S(10^{18})$.

## 解决方案

令$N=10^{18},M=\lfloor\sqrt[4]{N}\rfloor.$计算$S$时，我们考虑枚举每一个满立方数$w$，那么它们在$N$以内出现的次数为$\left\lfloor\dfrac{N}{w}\right\rfloor$.

通过考察$n$分解质因数$n=\prod_{i=1}^kp_i^{e_i}$的每个$e_i$，可以发现每一个满立方数可以通过$x^3y^4z^5$来**不重不漏**地表出，其中$x,y$是两个无平方因子数，并且$\gcd(x,y)=1.$

实现时，首先使用筛法将$M$以内的所有无平方因子数进行筛选出来。前两层循环分别枚举两个无平方因子数$z$和$y$。注意判断$\gcd(z,y)=1$时，只需要判断$zy$是否为无平方因子数即可，接下来直接枚举$x$，从而构造出一个满立方因子数$x^3y^4z^5$。

## 代码

```py
from itertools import count
from tools import int_sqrt

N = 10 ** 18
M = int(N ** (1 / 4))
square_free = [1] * (M + 1)
for i in range(2, int_sqrt(M) + 1):
    k = i * i
    for j in range(k, M + 1, k):
        square_free[j] = 0
ans = 0
for z in count(1, 1):
    z5 = z ** 5
    if z ** 5 > N:
        break
    if square_free[z]:
        for y in count(1, 1):
            y4 = y ** 4
            mul = y4 * z5
            if mul > N:
                break
            if square_free[y] and square_free[z * y]:
                for x in count(1, 1):
                    x3 = x ** 3
                    if mul * x3 > N:
                        break
                    ans += N // (mul * x3)
print(ans)

```
