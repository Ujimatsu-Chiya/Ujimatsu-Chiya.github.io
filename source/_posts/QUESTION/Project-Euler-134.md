---
title: Project Euler 134
category:
  - Project Euler
tags:
mathjax: true
date: 2022-05-06 22:22:59
---

<escape><!-- more --></escape>

# Project Euler 134

## 题目

### Prime pair connection

Consider the consecutive primes $p_1 = 19$ and $p_2 = 23$. It can be verified that $1219$ is the smallest number such that the last digits are formed by $p_1$ whilst also being divisible by $p_2$.

In fact, with the exception of $p_1 = 3$ and $p_2 = 5$, for every pair of consecutive primes, $p_2 > p_1$, there exist values of $n$ for which the last digits are formed by $p_1$ and $n$ is divisible by $p_2$. Let $S$ be the smallest of these values of $n$.

Find $\sum S$ for every pair of consecutive primes with $5 \leq p_1 \leq 1000000$.

## 解决方案

设$m$为$p_1$十进制下表示的长度（也就是$m=\lfloor\log_{10}n\rfloor+1$）

题目中的问题，可以转化为以下标准形式：求一个最小的非负整数$x$，使得$p_2\mid (p_1+10^mx)$

那么就转化成求线性同余方程$10^mx\equiv -p_1 \pmod {p_2}$。

这是一个线性同余方程$ax\equiv b \pmod m$的典型。解这类线性同余方程需要使用[扩展欧几里得](https://en.wikipedia.org/wiki/Extended_Euclidean_algorithm)算法辅助解决。

另外，如果$m$是一个质数，可以用费马小定理直接求解得$x\equiv a^{m-2}\cdot b \pmod m$。

最终求出$x$后，$S=10^mx+p_1$，对答案相加即可。

## 代码

```py
from tools import get_prime

N = 1000000
M = N + len(bin(N)) * 2 + 4
pr = get_prime(4, M)
ans = 0

for i in range(1, len(pr)):
    u, v = pr[i - 1], pr[i]
    if u > N:
        break
    pw = 10 ** len(str(u))
    x = (v - u) * pow(pw,v-2,v) % v
    s = pw * x + u
    ans += s
print(ans)

```
