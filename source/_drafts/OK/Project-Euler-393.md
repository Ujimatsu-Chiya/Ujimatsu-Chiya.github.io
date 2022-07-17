---
title: Project Euler 393
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    




# Project Euler 393
## 题目
### Migrating ants

An $n\times n$ grid of squares contains $n^2$ ants, one ant per square.

All ants decide to move simultaneously to an adjacent square (usually $4$ possibilities, except for ants on the edge of the grid or at the corners).

We define $f(n)$ to be the number of ways this can happen without any ants ending on the same square and without any two ants crossing the same edge between two squares.

You are given that $f(4) = 88$.

Find $f(10)$.


## 解决方案


## 代码


```py
from tools import get_pascals_triangle

N = 2022
mod = 10 ** 9 + 7
C = get_pascals_triangle(N, mod)
pw9 = [1]
for i in range(N + 1):
    pw9.append(pw9[-1] * 9 % mod)
ans = 0
for n in range(1, N + 1):
    for i in range(n // 2 + 1, n + 1):
        ans = (ans + pw9[n - i + 1] * C[n][i]) % mod
print(ans)

```