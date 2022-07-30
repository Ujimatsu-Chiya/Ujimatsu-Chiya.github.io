---
title: Project Euler 355
tags:
  - Project Euler
mathjax: true
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