---
title: Project Euler 81
tags:
  - Project Euler
  - 动态规划
mathjax: true
date: 2022-04-30 10:32:40
---

<escape><!-- more --></escape>

# Project Euler 81

## 题目

### Path sum: two ways

In the $5$ by $5$ matrix below, the minimal path sum from the top left to the bottom right, by **only moving to the right and down**, is indicated in bold red and is equal to $2427$.

$$
\begin{pmatrix}
\color{red}{131} & 673 & 234 & 103 & 18\\
\color{red}{201} & \color{red}{96} & \color{red}{342} & 965 & 150\\
630 & 803 & \color{red}{746} & \color{red}{422} & 111\\
537 & 699 & 497 & \color{red}{121} & 956\\
805 & 732 & 524 & \color{red}{37} & \color{red}{331}
\end{pmatrix}
$$

Find the minimal path sum, in [matrix.txt](../resources/p081_matrix.txt) (right click and “Save Link/Target As…”), a 31K text file containing a $80$ by $80$ matrix, from the top left to the bottom right by only moving right and down.

## 解决方案

本题是一道很明显的动态规划。

令矩阵大小为$n$，记录状态$f(i,j)(1\leq i,j\leq n)$为：当前走到第$i$行第$j$列的数的情况下，可以得到的路径最小和是多少，用$a[i][j]$表示第$i$行第$j$列的数。

那么，可以得到状态转移方程：

$$
f(i,j)=
\left \{\begin{aligned}
  &a[i][j]  & & \mathrm{if\quad} i=j=1 \\
  &f(i-1,j)+a[i][j] & & \mathrm{else if\quad} j=1 \\
  &f(i,j-1)+a[i][j] & & \mathrm{else if\quad} i=1 \\
  &\min(f(i,j-1),f(i-1,j)) + a[i][j] & & \mathrm{else}
\end{aligned}\right.
$$

对于有两种到达方式的状态，无非就是从上的格子走过来，和从左边的格子走过来两种。取这两种方式的较优决策即可。

最后答案为$f(n,n)$.

## 代码

```py
a = []
ls = open('p081_matrix.txt', 'r').readlines()
n = len(ls)
f = [[10 ** 10 for x in range(n)] for y in range(n)]
for i in range(n):
    b = [int(x) for x in ls[i][:-1].split(',')]
    a.append(b)

f = [[10 ** 10 for x in range(n + 1)] for y in range(n + 1)]
f[0][1] = 0
for i in range(1, n + 1):
    for j in range(1, n + 1):
        f[i][j] = min(f[i - 1][j], f[i][j - 1]) + a[i-1][j-1]
print(f[n][n])

```
