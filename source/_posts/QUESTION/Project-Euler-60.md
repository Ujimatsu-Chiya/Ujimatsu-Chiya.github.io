---
title: Project Euler 60
category:
  - Project Euler
tags:
  - 图论
mathjax: true
date: 2022-04-30 10:32:01
---

<escape><!-- more --></escape>

# Project Euler 60

## 题目

### Prime pair sets

The primes $3, 7, 109,$ and $673$, are quite remarkable. By taking any two primes and concatenating them in any order the result will always be prime. For example, taking $7$ and $109$, both $7109$ and $1097$ are prime. The sum of these four primes, $792$, represents the lowest sum for a set of four primes with this property.

Find the lowest sum for a set of five primes for which any two primes concatenate to produce another prime.

## 解决方案

本题的逼近上限难以通过分析方法计算出来，因此直接拟定一个上限，此处的上限定为$N=10^4$。

这题可以从图论的角度上考虑简化。如果质数对$(x,y)$满足题目条件，那么就将$x$和$y$连结一条边。

那么，这个问题就转化为，在这张图上面找一个大小为$5$的[团](https://en.wikipedia.org/wiki/Clique_(graph_theory))（团：无向图上的一个子图，但是这个子图是一个完全图。）

在我没有了解过networkx库时，我写了第一份代码，它是直接深度优先搜索寻找一个大小为$5$的团，并且没有添加太多的优化，最终运行了约$8$秒。

使用networkx的find_cliques函数，它可以找到图中的所有团。

另外，寻找图的最大团的算法为[Bron–Kerbosch algorithm](https://en.wikipedia.org/wiki/Bron%E2%80%93Kerbosch_algorithm)算法。networkx的find_cliques函数就是基于Bron-Kerbosch算法的迭代版本。

## 代码

```py
from tools import get_prime, is_prime

N = 10000
M = 5
pr = get_prime(N)

n = len(pr)
g = [[0 for i in range(n)] for j in range(n)]
for i in range(n):
    for j in range(i):
        x, y = pr[i], pr[j]
        u, v = int(str(x) + str(y)), int(str(y) + str(x))
        if is_prime(u) and is_prime(v):
            g[i][j] = g[j][i] = 1

a = [0 for i in range(M)]
ans = 0


def dfs(p: int, f: int):
    global ans
    if f == M:
        ans = sum([pr[x] for x in a])
        return 1
    while p < n:
        i = 0
        while i < f:
            if g[a[i]][p] == 0:
                break
            i += 1
        if i == f:
            a[f] = p
            if dfs(p + 1, f + 1):
                return 1
        p += 1
    return 0


dfs(0, 0)
print(ans)
```

```py
from tools import get_prime, is_prime
import networkx as nx

G = nx.Graph()
N = 10000
M = 5
pr = get_prime(N)

n = len(pr)
for i in range(n):
    for j in range(i):
        x, y = pr[i], pr[j]
        u, v = int(str(x) + str(y)), int(str(y) + str(x))
        if is_prime(u) and is_prime(v):
            G.add_edge(i, j)

a = [b for b in nx.find_cliques(G) if len(b) == M]
ans = min((sum(pr[x] for x in pos) for pos in a))
print(ans)
```
