---
title: Project Euler 215
category:
  - Project Euler
tags:
  - 动态规划
mathjax: true
date: 2022-07-01 17:37:15
---

<escape><!-- more --></escape>

# Project Euler 215

## 题目

### Crack-free Walls

Consider the problem of building a wall out of $2\times1$ and $3\times1$ bricks (horizontal\timesvertical dimensions) such that, for extra strength, the gaps between horizontally-adjacent bricks never line up in consecutive layers, i.e. never form a "running crack".

For example, the following $9\times3$ wall is not acceptable due to the running crack shown in red:

![](../images/p215_crackfree.gif)

There are eight ways of forming a crack-free $9\times3$ wall, written $W(9,3) = 8$.

Calculate $W(32,10)$.

## 解决方案

令$N=32,M=10$。先将每一行可能的状态都搜索出来，存入一个下标起始为$1$的数组$st$中。这些状态用一个$N-1$位二进制数$b=b_{N-1}b_{N-2}\dots b_2b_1$保存。其中，如果第$k$列有空隙，那么$b_k=1$，否则$b_k=0$。令$m$为数组$st$的长度。

那么，如果一行的墙砖$st[i]$可以拼接在$st[j]$的下面，那么$st[j]\&st[i]=0$。这里的$\&$为与运算。这题就可以使用动态规划的思想轻易解决。

假设$f(i,j)(1\le i\le M,1\le j\le m)$为已经铺好了前$i$行，其中第$i$行的状态为$st[j]$，那么可以列出如下状态转移方程：

$$
f(i,j)=
\left \{\begin{aligned}
  &1  & & \text{if}\quad i=1 \\
  &\sum_{st[j]\&st[k]=0}  f(i-1,k) & & \text{else}
\end{aligned}\right.
$$

最终答案为$\sum_{j=1}^m f(M,j)$。

## 代码

```py
M = 32
N = 10


def gen(M):
    st = []

    def dfs(f, s):
        if f > M:
            return
        elif f == M:
            st.append(s ^ 1 << M)
            return
        dfs(f + 2, s | 1 << (f + 2))
        dfs(f + 3, s | 1 << (f + 3))

    dfs(0, 0)
    return st


st = gen(M)
g = [[] for _ in range(len(st))]
for i in range(len(st)):
    for j in range(i + 1, len(st)):
        if (st[i] & st[j]) == 0:
            g[i].append(j)
            g[j].append(i)
f = [1] * len(st)
for i in range(N-1):
    f = [sum(f[j] for j in g[i]) for i in range(len(st))]
ans = sum(f)
print(ans)

```
