---
title: Project Euler 83
category:
  - Project Euler
tags:
  - 图论
mathjax: true
date: 2022-04-30 10:32:48
---

<escape><!-- more --></escape>

# Project Euler 83

## 题目

### Path sum: four ways

NOTE: This problem is a significantly more challenging version of [Problem 81](../Project-Euler-81).

In the $5$ by $5$ matrix below, the minimal path sum from the top left to the bottom right, by moving left, right, up, and down, is indicated in bold red and is equal to $2297$.

$$\begin{pmatrix}
\color{red}{131} & 673 & \color{red}{234} & \color{red}{103} & \color{red}{18}\\
\color{red}{201} & \color{red}{96} & \color{red}{342} & 965 & \color{red}{150}\\
630 & 803 & 746 & \color{red}{422} & \color{red}{111}\\
537 & 699 & 497 & \color{red}{121} & 956\\
805 & 732 & 524 & \color{red}{37} & \color{red}{331}
\end{pmatrix}$$

Find the minimal path sum from the top left to the bottom right by moving left, right, up, and down in [matrix.txt](../resources/p081_matrix.txt) (right click and "Save Link/Target As..."), a 31K text file containing an $80$ by $80$ matrix.

## 解决方案

本题不再适用于动态规划的做法，因为不能够很好地分阶段。

注意到，本题求的是最小值。因此，可以将整个模型转化为图论的单源最短路去完成。

令矩阵大小为$n$。把矩阵中的每一个元素视为一个节点，那么就是求节点$(1,1)$到节点$(n,n)$的最短路径。注意到这里使用的是有向图，边集如下构造：
对于矩阵中所有元素，都有$4$条出边指向其四个方向的相邻元素，边权为指向的元素的值。

最终，计算出$(1,1)$到$(n,n)$的最短路径长度再加上$(1,1)$元素本身的值，就是最终答案。

单源最短路以[Dijkstra](https://en.wikipedia.org/wiki/Dijkstra%27s_algorithm)，[Bellman-Ford](https://en.wikipedia.org/wiki/Bellman%E2%80%93Ford_algorithm)为代表。多源最短路则以[Floyd](https://en.wikipedia.org/wiki/Floyd%E2%80%93Warshall_algorithm)为代表。

本代码实现主要使用`networkx`库利用`Dijkstra`算法导出结果。

## 代码

```py
import networkx as nx

ls = open('p081_matrix.txt', 'r').readlines()
n = len(ls)
a = []
for i in range(n):
    b = [int(x) for x in ls[i][:-1].split(',')]
    a.append(b)
g = nx.DiGraph()
d = [[-1, 0], [1, 0], [0, -1], [0, 1]]

for i in range(n):
    for j in range(n):
        for dx, dy in d:
            x, y = i + dx, j + dy
            if 0 <= x < n and 0 <= y < n:
                g.add_edge((i, j), (x, y), weight=a[x][y])
ans = nx.dijkstra_path_length(g, (0, 0), (n - 1, n - 1)) + a[0][0]
print(ans)
```
