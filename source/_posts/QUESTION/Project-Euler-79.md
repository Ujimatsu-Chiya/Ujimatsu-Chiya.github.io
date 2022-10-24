---
title: Project Euler 79
category:
  - Project Euler
tags:
  - 图论
mathjax: true
date: 2022-04-30 10:32:36
---

<escape><!-- more --></escape>

# Project Euler 79

## 题目

### Passcode derivation

A common security method used for online banking is to ask the user for three random characters from a passcode. For example, if the passcode was $531278$, they may ask for the $2\text{nd}$, $3\text{rd}$, and $5\text{th}$ characters; the expected reply would be: $317$.

The text file, [keylog.txt](../resources/p079_keylog.txt), contains fifty successful login attempts.

Given that the three characters are always asked for in order, analyse the file so as to determine the shortest possible secret passcode of unknown length.

## 解决方案

本题的解题方法依赖于这个假设：所有密码位的出现都是唯一的。

因此，可以通过[建立有向无环图（DAG）](https://en.wikipedia.org/wiki/Directed_acyclic_graph)，表示密码位的关系。（如果这不是一个DAG，那么上述事实不成立）

如$317$，则将连接两条有向边$3\rightarrow 1,1\rightarrow 7$。

对最终建成的DAG进行[拓扑排序](https://en.wikipedia.org/wiki/Topological_sorting)，得到的即为最终答案（如果拓扑排序失败，说明这不是一个DAG）。

以下是维基百科中，关于拓扑排序算法的伪代码：

```
L ← Empty list that will contain the sorted elements
S ← Set of all nodes with no incoming edge

while S is not empty do
    remove a node n from S
    add n to L
    for each node m with an edge e from n to m do
        remove edge e from the graph
        if m has no other incoming edges then
            insert m into S

if graph has edges then
    return error   (graph has at least one cycle)
else 
    return L (a topologically sorted order)
```

本代码中将实现两种方式：手动实现拓扑排序和使用`networkx`库导出。

## 代码

```py
from queue import Queue

g = [[] for i in range(10)]
d = [0 for i in range(10)]
f = [0 for i in range(10)]
ls = open('p079_keylog.txt', 'r').readlines()
for s in ls:
    x = int(s[:-1])
    a = x // 100
    b = x // 10 % 10
    c = x % 10
    g[a].append(b)
    g[b].append(c)
    d[b] += 1
    d[c] += 1
    f[a] = f[b] = f[c] = 1
q = Queue()
for i in range(10):
    if d[i] == 0 and f[i]:
        q.put(i)

a = []
while not q.empty():
    u = q.get()
    a.append(u)
    for v in g[u]:
        d[v] -= 1
        if d[v] == 0:
            q.put(v)
ans = "".join(str(x) for x in a)
print(ans)
```

```py
import networkx as nx

g = nx.DiGraph()
for s in open('p079_keylog.txt', 'r').readlines():
    g.add_edge(s[0], s[1])
    g.add_edge(s[1], s[2])

ans = "".join(list(nx.topological_sort(g)))
print(ans)
```
