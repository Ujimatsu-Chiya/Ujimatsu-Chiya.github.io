---
title: Project Euler 212
category:
  - Project Euler
tags:
  - 容斥原理
mathjax: true
date: 2022-07-01 17:37:11
---

<escape><!-- more --></escape>

# Project Euler 212

## 题目

### Combined Volume of Cuboids

An *axis-aligned cuboid*, specified by parameters $\{ (x_0,y_0,z_0), (dx,dy,dz) \}$, consists of all points $(X,Y,Z)$ such that $x_0 \le X \le x_0+dx, y_0 \le Y \le y_0+dy$ and $z_0 \le Z \le z_0+dz$.  The volume of the cuboid is the product, $dx \times dy \times dz$.  The *combined volume* of a collection of cuboids is the volume of their union and will be less than the sum of the individual volumes if any cuboids overlap.

Let $C_1,\dots,C_{50000}$ be a collection of $50000$ axis-aligned cuboids such that $C_n$ has parameters

$\begin{aligned}
x_0 &=& S_{6n-5} \text{ modulo } 10000\\
y_0 &=& S_{6n-4} \text{ modulo } 10000\\
z_0 &=& S_{6n-3} \text{ modulo } 10000\\
dx &=& 1 + (S_{6n-2} \text{ modulo } 399)\\
dy &=& 1 + (S_{6n-1} \text{ modulo } 399)\\
dz &=& 1 + (S_{6n} \text{ modulo } 399)
\end{aligned}$

where $S_1,\dots,S_{300000}$ come from the “Lagged Fibonacci Generator”:

For $1 \le k \le 55, S_k = [100003 - 200003k + 300007k^3]  (\text{ modulo } 1000000)$

For $56 \le k, S_k = [S_{k-24} + S_{k-55}] (\text{ modulo } 1000000)$

Thus, $C_1$ has parameters $\{(7,53,183),(94,369,56)\}$, $C_2$ has parameters $\{(2383,3563,5079),(42,212,344)\}$, and so on.

The combined volume of the first $100$ cuboids, $C_1,\dots,C_{100}$, is $723581599$.

What is the combined volume of all $50000$ cuboids, $C_1,\dots,C_{50000}$ ?

## 解决方案

这$50000$个方块有以下特点：

1. 它们是用**伪随机**算法“均匀”生成的，因此实际上，被方块占领的空间相对均匀。
2. 这些方块的边长很小（最多$399$），但是空间长度却很大（最多可以达到$10399$）。

因此，我们可以将整个空间划分成多个部分，然后分别在每个部分中计算体积，最终再求和。并且，对于任何一个划分出来的空间，立方体的数量比较少（这说明我们在后面使用容斥原理时，枚举量将很少）。

这里的划分方案是：每一个部分将划分成$B\times B\times B$的大小，其中$B=399$。这种划分方式保证了每一个方块最多只会被划分成$8$部分。

对于每一个划分出来的空间而言，考虑使用容斥原理进行计算这一部分的体积：如果当前空间是奇数个方块的**交集**，那么这个交集的体积就需要在答案中加上，否则就从答案中减去。以此过程最终计算出答案。

当然，本题也可以用八叉树进行实现，不过效率较低。

## 代码

```py
from collections import defaultdict

N = 50000
block = 399


def gen():
    a = []
    for i in range(1, 56):
        a.append((100003 - 200003 * i + 300007 * i ** 3) % 1000000)
        yield a[-1]
    while True:
        a.append((a[-24] + a[-55]) % 1000000)
        yield a[-1]


def dfs(f, flag, pre, here):
    s = 0
    for i in range(f, len(here)):
        now = cubes[here[i]]
        x, y, z = max(pre[0], now[0]), max(pre[1], now[1]), max(pre[2], now[2])
        dx = min(pre[0] + pre[3], now[0] + now[3]) - x
        dy = min(pre[1] + pre[4], now[1] + now[4]) - y
        dz = min(pre[2] + pre[5], now[2] + now[5]) - z
        if min(dx, dy, dz) <= 0:
            continue
        s += flag * dx * dy * dz + dfs(i + 1, -flag, [x, y, z, dx, dy, dz], here)
    return s


cubes = []
mp = defaultdict(list)
g = gen()

for m in range(N):
    a, b, c = g.__next__() % 10000, g.__next__() % 10000, g.__next__() % 10000
    x, y, z = g.__next__() % 399 + 1, g.__next__() % 399 + 1, g.__next__() % 399 + 1
    cubes.append((a, b, c, x, y, z))
    for i in range(a // block, (a + x) // block + 1):
        for j in range(b // block, (b + y) // block + 1):
            for k in range(c // block, (c + z) // block + 1):
                mp[i, j, k].append(m)
ans = 0
for pos, here in mp.items():
    ans += dfs(0, 1, [pos[0] * block, pos[1] * block, pos[2] * block, block, block, block], here)
print(ans)

```
