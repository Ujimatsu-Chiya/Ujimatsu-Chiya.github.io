---
title: Project Euler 62
tags:
  - Project Euler
mathjax: true
date: 2022-04-30 10:32:08
---

<escape><!-- more --></escape>

# Project Euler 62

## 题目

### Cubic permutations

The cube, $41063625$ ($345^3$), can be permuted to produce two other cubes: $56623104$ ($384^3$) and $66430125$ ($405^3$). In fact, $41063625$ is the smallest cube which has exactly three permutations of its digits which are also cube.

Find the smallest cube for which exactly five permutations of its digits are cube.

## 解决方案

从小到大找出立方数。将使用数位的立方数汇总到一起。

如果其中一个集合先汇总了$5$个立方数，那么就输出最小的。

## 代码

```py
from itertools import count

N = 5
mp = {}
for i in count(1, 1):
    u = "".join((lambda x: (x.sort(), x)[1])(list(str(i * i * i))))
    if u not in mp.keys():
        mp[u] = []
    mp[u].append(i * i * i)
    if len(mp[u]) == N:
        ans = mp[u][0]
        break

print(ans)
```
