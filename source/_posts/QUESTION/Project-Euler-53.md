---
title: Project Euler 53
category:
  - Project Euler
tags:
mathjax: true
date: 2022-04-30 10:31:32
---

<escape><!-- more --></escape>

# Project Euler 53

## 题目

### Combinatoric selections

There are exactly ten ways of selecting three from five, $12345$:

$$ 123, 124, 125, 134, 135, 145, 234, 235, 245, 345 $$

In combinatorics, we use the notation, $\displaystyle \binom 5 3 = 10$.
In general, $\displaystyle \binom n r = \dfrac{n!}{r!(n-r)!}$, where $r \le n$, $n! = n \times (n-1) \times \dots \times 3 \times 2 \times 1$, and $0! = 1$.

It is not until $n = 23$, that a value exceeds one-million: $\displaystyle \binom {23} {10} = 1144066$.

How many, not necessarily distinct, values of $\displaystyle \binom n r$ for $1 \le n \le 100$, are greater than one-million?

## 解决方案

根据组合数的递推式，计算出[杨辉三角](https://mathworld.wolfram.com/PascalsTriangle.html)前$101$行的值。

由于`Python`支持计算大数，因此直接进行枚举判断。

产生杨辉三角的方法将会被封装在自定义的`tools`工具包中，以`get_pascals_triangle(n,mod=None)`获得杨辉三角的前$n+1$行，其中所有值对`mod`取模。

## 代码

```py
N = 100
M = 10 ** 6
ans = 0

C = [[0 for y in range(x + 1)] for x in range(N + 1)]
for i in range(N + 1):
    C[i][0] = C[i][i] = 1
    for j in range(1, i):
        C[i][j] = C[i - 1][j - 1] + C[i - 1][j]
    if i > 0:
        ans += sum(1 for j in range(i + 1) if C[i][j] >= M)
print(ans)

```
