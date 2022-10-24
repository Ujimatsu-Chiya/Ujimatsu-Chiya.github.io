---
title: Project Euler 349
category:
  - Project Euler
tags:
mathjax: true
date: 2022-07-08 17:06:35
---

<escape><!-- more --></escape>

# Project Euler 349

## 题目

### Langton's ant

An ant moves on a regular grid of squares that are coloured either black or white.

The ant is always oriented in one of the cardinal directions (left, right, up or down) and moves from square to adjacent square according to the following rules:

- if it is on a black square, it flips the colour of the square to white, rotates $90$ degrees counterclockwise and moves forward one square.
- if it is on a white square, it flips the colour of the square to black, rotates $90$ degrees clockwise and moves forward one square.

Starting with a grid that is entirely white, how many squares are black after $10^{18}$ moves of the ant?

## 解决方案

如果当前是从白色格子转成黑色格子，那么在序列中记录一个值$1$，如果是黑色格子，那么记录一个值$-1$。

最终，记录的这些值之和就是黑色格子数。

考虑直接模拟这只蚂蚁的行为。本代码打印了蚂蚁的前$m=20000$步数的踪迹，发现在第约$10000$步时，记录的这个序列开始循环，其周期为$T=104$，并且在每个周期中，黑色格子每次增加$12$个。

那么，本题直接枚举$m$步以内的所有颜色变化情况，之后的所有部分通过周期直接分块计算即可。

## 代码

```py
from collections import defaultdict

N = 10 ** 18
mp = defaultdict(int)
dx, dy = [-1, 0, 1, 0], [0, -1, 0, 1]
x, y, k = 0, 0, 0
a = []
m = 20000
T = 104
for i in range(m):
    if mp[x, y] == 0:
        k = (k - 1) & 3
        a.append(1)
    else:
        k = (k + 1) & 3
        a.append(-1)
    mp[x, y] ^= 1
    x += dx[k]
    y += dy[k]
# print(a) 查看前m步的颜色变化情况。
ans = sum(a[:min(m, N)])
N -= min(N, m)
a = a[-T:]
block, res = N // T, N % T
ans += sum(a) * block + sum(a[:res])
print(ans)

```
