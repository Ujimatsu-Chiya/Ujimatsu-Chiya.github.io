---
title: Project Euler 110
tags:
  - Project Euler
mathjax: true
date: 2022-05-06 22:23:54
---

<escape><!-- more --></escape>

# Project Euler 110

## 题目

### Diophantine reciprocals II

In the following equation $x, y$, and $n$ are positive integers.

$$\dfrac{1}{x} + \dfrac{1}{y} = \dfrac{1}{n}$$

It can be verified that when $n = 1260$ there are 113 distinct solutions and this is the least value of $n$ for which the total number of distinct solutions exceeds one hundred.

What is the least value of $n$ for which the number of distinct solutions exceeds four million?

<p class="smaller">NOTE: This problem is a much more difficult version of <a href="problem=108">Problem 108</a> and as it is well beyond the limitations of a brute force approach it requires a clever implementation.

## 解决方案

使用的方案和第108题完全相同，此处不赘述。

## 代码

```py
from tools import get_prime

N = 4000000
pr = get_prime(len(bin(N)) * 50)
ans = N ** 10


def dfs(n: int, mul: int, f: int, lm: int):
    global ans
    if (mul + 1) >> 1 >= N:
        ans = n
        return
    for i in range(1, lm + 1):
        n *= pr[f]
        if n > ans:
            break
        dfs(n, mul * (2 * i + 1), f + 1, i)


dfs(1, 1, 0, N)
print(ans)

```
