---
title: Project Euler 171
tags:
  - Project Euler
  - 动态规划
mathjax: true
date: 2022-05-15 10:15:56
---

<escape><!-- more --></escape>

# Project Euler 171

## 题目

### Finding numbers for which the sum of the squares of the digits is a square

For a positive integer $n$, let $f(n)$ be the sum of the squares of the digits (in base $10$) of n, e.g.

$\begin{aligned}
& f(3) = 3^2 = 9, \\
& f(25) = 2^2 + 5^2 = 4 + 25 = 29, \\
& f(442) = 4^2 + 4^2 + 2^2 = 16 + 16 + 4 = 36
\end{aligned}$

Find the last nine digits of the sum of all $n$, $0 < n < 10^{20}$, such that $f(n)$ is a perfect square.

## 解决方案

一道非常明显的数位动态规划题目。不过，这里要求我们统计的是满足条件的数的和。

我们可以通过先统计个数，计算出每个数位上的数的贡献次数，从而计算出它们的和。

设$N=20$。令$c(i,j)(1\le i\le N,0\le j\le 9^2\cdot i)$表示$i$位数中，有多少个数的函数值$f$为$j$。不难列出以下状态转移方程：

$$
c(i,j)=
\left \{\begin{aligned}
  &1  & & \mathrm{if\quad} i=1\&j\in\{x^2\mid x\in \mathbb{N},1\le x\le 9\} \\
  &0 & & \mathrm{else if\quad} i=1\\
  &\sum_{k=0}^{\min(9,\lfloor\sqrt{j}\rfloor)}c(i-1,j-k^2) & & \mathrm{else}
\end{aligned}\right.
$$

其中，最后一行表示，每一个数都可以添加一个数位$k$在其后面，那么$f$就会增加$k^2$。

根据符合状态的数的出现次数，可以确定每一个数位的贡献。令$s(i,j)(1\le i\le N,0\le j\le 9^2\cdot i)$表示$i$位数中，函数值$f$为$j$的所有数之和，那么可以列出以下状态转移方程：

$$
s(i,j)=
\left \{\begin{aligned}
  &\sqrt{j}  & & \mathrm{if\quad} i=1\&j\in\{x^2\mid x\in \mathbb{N},1\le x\le 9\} \\
  &0 & & \mathrm{else if\quad} i=1\\
  &\sum_{k=0}^{\min(9,\lfloor\sqrt{j}\rfloor)}10\cdot s(i-1,j-k^2)+k\cdot c(i-1,j-k^2) & & \mathrm{else}
\end{aligned}\right.
$$

最后一行中，将$c(i-1,j-k^2)$个数后面都放置一个$k$，就可以产生贡献，而之前的数就需要向前进一位，乘$10$。

最终答案为：
$$\sum_{i=1}^N\sum_{j=0}^{\lfloor9\sqrt{i}\rfloor}s(i,j^2)$$

## 代码

```py
from itertools import count

N = 20
mod = 10 ** 9
c = [[0 for _ in range(N * 9 * 9 + 1)] for _ in range(N + 1)]
s = [[0 for _ in range(N * 9 * 9 + 1)] for _ in range(N + 1)]
for j in range(1, 10):
    c[1][j * j] = 1
    s[1][j * j] = j

for i in range(2, N + 1):
    for j in range(i * 9 * 9 + 1):
        for k in range(10):
            if j - k * k < 0:
                break
            c[i][j] += c[i - 1][j - k * k]
            s[i][j] += s[i - 1][j - k * k] * 10 + k * c[i - 1][j - k * k]
ans = 0
for j in count(1, 1):
    if j * j > 9 * 9 * N:
        break
    for i in range(1, N + 1):
        ans += s[i][j * j]
ans %= mod
print(ans)

```
