---
title: Project Euler 265
tags:
  - Project Euler
mathjax: true
date: 2022-07-04 18:02:09
---

<escape><!-- more --></escape>

# Project Euler 265

## 题目

### Binary Circles

$2^N$ binary digits can be placed in a circle so that all the $N$-digit clockwise subsequences are distinct.

For $N=3$, two such circular arrangements are possible, ignoring rotations:

![](../images/p265_BinaryCircles.gif)

For the first arrangement, the $3$-digit subsequences, in clockwise order, are: $000, 001, 010, 101, 011, 111, 110$ and $100$.

Each circular arrangement can be encoded as a number by concatenating the binary digits starting with the subsequence of all zeros as the most significant bits and proceeding clockwise. The two arrangements for $N=3$ are thus represented as $23$ and $29$:

$$\begin{aligned}
00010111_2 = 23\\
00011101_2 = 29
\end{aligned}$$

Calling $S(N)$ the sum of the unique numeric representations, we can see that $S(3) = 23 + 29 = 52$.
Find $S(5)$.

## 解决方案

本题没有太多需要注意的地方。直接把一个个二进制数视为一个节点，每个节点都有两条出边。然后再在图上寻找[哈密顿回路](https://en.wikipedia.org/wiki/Hamiltonian_path)即可。

OEIS上的数列[A016031](https://oeis.org/A016031)提到，$2^N$个$N$比特串上述的环排列一共有$2^{2^{N-1}-N}$个。

## 代码

```py
N = 5
M = 1 << N
mask = (1 << N) - 1
g = [[i << 1 & mask, (i << 1 | 1) & mask] for i in range(M)]
vis = [0 for i in range(M)]
vis[0] = 1
ans = 0


def dfs(f: int, u: int, s: int):
    if f == M - 1:
        if u == (M >> 1):
            global ans
            ans += s >> (N - 1)
        return
    for v in g[u]:
        if vis[v]:
            continue
        vis[v] = 1
        dfs(f + 1, v, s << 1 | (v & 1))
        vis[v] = 0


dfs(0, 0, 0)
print(ans)

```
