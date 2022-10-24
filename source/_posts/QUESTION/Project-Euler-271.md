---
title: Project Euler 271
category:
  - Project Euler
tags:
  - 中国剩余定理
mathjax: true
date: 2022-07-06 13:08:28
---

<escape><!-- more --></escape>

# Project Euler 271

## 题目

### Modular Cubes, part $1$

For a positive number $n$, define $S(n)$ as the sum of the integers $x$, for which $1<x<n$ and $x^3\equiv 1 \bmod n$.

When $n=91$, there are $8$ possible values for $x$, namely : $9, 16, 22, 29, 53, 74, 79, 81$.

Thus, $S(91)=9+16+22+29+53+74+79+81=363$.

Find $S(13082761331670030)$.

## 解决方案

写在前面：

比较投机取巧的一种方法：直接使用`sympy.ntheory.residue_ntheory`库中的`nthroot_mod`方法。

这个方法主要传入三个参数：`nthroot_mod(a,n,p)`，用来求解三次剩余$x^n\equiv a \pmod p$.

平常做法：

首先将$n=13082761331670030$进行分解，得到$n=\prod_{i=1}^k p_i^{e_i}$.

那么，求解$x^3\equiv1\pmod n$就变成了求解一系列的$x_i^3\equiv 1\pmod {p_i^{e_i}}$，然后再分别将所有解通过[中国剩余定理](https://mathworld.wolfram.com/ChineseRemainderTheorem.html)重新合并起来，就变成了原方程的解。

并且，可以发现题目中给定的$n$，所有的$p_e^{e_i}$都很小。实际上，所有的$e_i$都为$1$，因此求解$x_i^3\equiv 1\pmod {p_i^{e_i}}$使用的是暴力枚举。

## 代码

```py
from sympy.ntheory.residue_ntheory import nthroot_mod

N = 13082761331670030
ans = sum(nthroot_mod(1, 3, N, all_roots=True)) - 1
print(ans)

```

```py
from itertools import product
from tools import factorization
from sympy import mod_inverse
import functools, operator

N = 13082761331670030


def CRT(a, p):
    M = functools.reduce(operator.mul, p, 1)
    m_inv = [mod_inverse(M // x, x) for x in p]
    return sum(a[i] * m_inv[i] * M // p[i] for i in range(len(a))) % M


pe = []
sol = []
for p, e in factorization(N):
    n = p ** e
    pe.append(n)
    sol.append([x for x in range(n) if pow(x, 3, n) == 1])
ans = sum(CRT(a, pe) for a in product(*sol)) - 1
print(ans)

```
