---
title: Project Euler 82
tags:
  - Project Euler
  - 动态规划
mathjax: true
date: 2022-04-30 10:32:44
---

<escape><!-- more --></escape>

# Project Euler 82

## 题目

### Path sum: three ways

NOTE: This problem is a more challenging version of <a href="problem=81">Problem 81</a>.

The minimal path sum in the $5$ by $5$ matrix below, by starting in any cell in the left column and finishing in any cell in the right column, and only moving up, down, and right, is indicated in red and bold; the sum is equal to $994$.

$$
\begin{pmatrix}
131 & 673 & \color{red}{234} & \color{red}{103} & \color{red}{18}\\
\color{red}{201} & \color{red}{96} & \color{red}{342} & 965 & 150\\
630 & 803 & 746 & 422 & 111\\
537 & 699 & 497 & 121 & 956\\
805 & 732 & 524 & 37 & 331
\end{pmatrix}
$$

Find the minimal path sum from the left column to the right column in [matrix.txt](../resources/p081_matrix.txt) (right click and "Save Link/Target As..."), a 31K text file containing an $80$ by $80$ matrix.

## 解决方案

本题用动态规划的思想解决。

本题的动态规划可以以一列列作为阶段。因为每一条从最左列到最右列的路径，可以视为是**一个个列的连续子数组**拼接而成。而且由于只能向右走，路径上所处的每一列，它们的**行下标都是首尾相接**的。
如果往上走，或者是往下走，就能够走出一个**列上的子数组**。

以上图为例，红色路径上的列子数组从左到右分别为$[201],[96],[342,234],[103],[18]$，而且它们的行下标是首尾相接的。

因此，记录状态$f(i,j)(1\leq i,j\leq n)$为：表示当前走到第j列的情况下，在这一列以第i行为终点时路径的最小和，用$a[i][j]$表示第$i$行第$j$列的数。

那么，可以得到状态转移方程：

$$
f(i,j)=
\left \{\begin{aligned}
  &a[i][j]  & & \mathrm{if\quad} j=1 \\
  &\min_{k=1}^n (f(k,j-1)+\sum_{p=\min(i,k)}^{\max(i,k)} a[p][j]) & & \mathrm{else}
\end{aligned}\right.
$$
在该状态转移方程中，$k$是指当前左边那一列的“终点”，也就是本列的起点。

为求列的子数组和，可以用一个前缀和预处理。

最终答案为$min_{i=1}^n(f(i,n))$。

## 代码

```py
a = []
ls = open('p081_matrix.txt', 'r').readlines()
n = len(ls)
f = [[10 ** 10 for x in range(n)] for y in range(n)]
for i in range(n):
    b = [int(x) for x in ls[i][:-1].split(',')]
    a.append(b)

f = [[0 for j in range(n + 1)] for i in range(n + 1)]
s = [[0 for j in range(n + 1)] for i in range(n + 1)]
for i in range(1, n + 1):
    for j in range(1, n + 1):
        s[i][j] = s[i - 1][j] + a[i - 1][j - 1]

for i in range(1, n + 1):
    f[i][1] = a[i - 1][0]

for j in range(2, n + 1):
    for i in range(1, n + 1):
        f[i][j] = min(f[k][j - 1] + s[max(i, k)][j] - s[min(i, k) - 1][j] for k in range(1, n + 1))

ans = min(f[i][n] for i in range(1, n + 1))
print(ans)

```
