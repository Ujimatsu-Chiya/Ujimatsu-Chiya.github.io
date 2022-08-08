---
title: Project Euler 130
category:
  - Project Euler
tags:
mathjax: true
date: 2022-05-08 11:56:02
---

<escape><!-- more --></escape>

# Project Euler 130

## 题目

### Composites with prime repunit property

A number consisting entirely of ones is called a repunit. We shall define $R(k)$ to be a repunit of length $k$; for example, $R(6) = 111111$.

Given that $n$ is a positive integer and $\gcd(n, 10) = 1$, it can be shown that there always exists a value, $k$, for which $R(k)$ is divisible by $n$, and let $A(n)$ be the least such value of $k$; for example, $A(7) = 6$ and $A(41) = 5$.

You are given that for all primes, $p > 5$, that $p − 1$ is divisible by $A(p)$. For example, when $p = 41$, $A(41) = 5$, and $40$ is divisible by $5$.

However, there are rare composite values for which this is also true; the first five examples being $91$, $259$, $451$, $481$, and $703$.

Find the sum of the first twenty-five composite values of $n$ for which $\gcd(n, 10) = 1$ and $n − 1$ is divisible by $A(n)$.

## 解决方案

明显注意到对于正整数$k$，$3|k\Leftrightarrow3|R(k)$。

因此，如果$k$是$3$的倍数，那么$A(k)$也必须是$3$的倍数，但是此时$k-1$不是$3$的倍数，它不能被$A(k)$整除。

本代码将枚举所有正整数$m$满足于$m\equiv 5(\mod 6)$。然后再判断$m$是否为合数。如果是合数，再判断$A(n)$是否为$n-1$的因子。

计算$A(m)$的方式和129题相同，使用sympy库中的n_order(a,m)函数计算元素阶$\lambda_m(a)$的值。

## 代码

```py
from itertools import count

from sympy import n_order
from tools import is_prime

Q = 25
ls = []
for n in count(7, 2):
    if n % 5 == 0 or n % 3 == 0 or is_prime(n):
        continue
    order = n_order(10, n * 9)
    if (n - 1) % order == 0:
        ls.append(n)
    if len(ls) == Q:
        break
ans = sum(ls)
print(ans)

```
