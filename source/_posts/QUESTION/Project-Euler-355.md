---
title: Project Euler 355
tags:
  - Project Euler
mathjax: true
date: 2022-08-05 21:41:48
---

<escape><!-- more --></escape>

# Project Euler 355

## 题目

### Maximal coprime subset

Define $Co(n)$ to be the maximal possible sum of a set of mutually co-prime elements from $\{1, 2, \dots, n\}$.

 For example $Co(10)$ is $30$ and hits that maximum on the subset $\{1, 5, 7, 8, 9\}$.

You are given that $Co(30) = 193$ and $Co(100) = 1356$.

Find $Co(200000)$.

## 解决方案

令$N=200000$，令函数$f(n,p)$表示求$p$最大的质数幂$p^k\le n$。

本题基于这个假设完成：被选上集合的数$n$，必定是以下两类数之一：

- $f(n,p)$.对于$N$以内的任何一个质数$p$。
- $f(\lfloor\dfrac{n}{q}\rfloor,p)\cdot q$，其中$p$是一个质数，$q$是一个大于$\lfloor\sqrt{N}\rfloor$的质数。

如果质数$p,q$构造出了候选答案的第二类数，那么其它第二类数必定不能含有$p,q$这两个质因子，因此我们可以将其转化成[最小费用最大流问题](https://en.wikipedia.org/wiki/Minimum-cost_flow_problem)来解决。一开始我们先假设候选答案中只有第一类数，其总和为$s$，往后再逐渐添加第二类数。

假设小于等于$\lfloor\sqrt{N}\rfloor$的质数为集合$P$，其余质数为集合$Q$。对于$p\in P,q \in Q$，如果$f(\lfloor\dfrac{n}{q}\rfloor)\cdot p>f(n,p)+q$，那么从节点$p$到节点$q$连一条容量为$1$，费用为$-(f(\lfloor\dfrac{n}{q}\rfloor)\cdot p-f(n,p)-q)$的边。那么，将源点连向$P$中的每个节点，将$Q$中的每个节点连向汇点，这些边的容量都为$1$，费用都为$0$。

最终使用networkx库中的max_flow_min_cost方法完成计算。将答案添加到$s$中，成为最终答案。需要注意的是，我们求的费用是最大值，因此整张图的费用权值都是负数。

## 代码

```py
from tools import get_prime
import networkx as nx

N = 200000


def cal(n, p):
    m = 1
    while m * p <= n:
        m *= p
    return m


pr = get_prime(N)
g = nx.DiGraph()
ans = 1
st, ed = [], []
s, t = -1, -2
for p in pr:
    ans += cal(N, p)
    if p ** 2 <= N:
        g.add_edge(s, p, capacity=1, weight=0)
        st.append(p)
    elif p + p <= N:
        g.add_edge(p, t, capacity=1, weight=0)
        ed.append(p)
for p in st:
    for q in ed:
        if p * q > N:
            break
        k = cal(N // q, p) * q
        if cal(N, p) + q < k:
            g.add_edge(p, q, capacity=1, weight=-(k - cal(N, p) - q))

ans += -nx.cost_of_flow(g, nx.max_flow_min_cost(g, s, t))
print(ans)

```
