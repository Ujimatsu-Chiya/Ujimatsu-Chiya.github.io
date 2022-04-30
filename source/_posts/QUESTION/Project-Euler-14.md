---
title: Project Euler 14
tags:
  - Project Euler
mathjax: true
date: 2022-04-26 18:35:45
---

<escape><!-- more --></escape>

# Project Euler 14

## 题目

### Longest Collatz sequence

The following iterative sequence is defined for the set of positive integers:
$n \rightarrow n/2$ ($n$ is even)<br>$n \rightarrow 3n + 1$ ($n$ is odd)
Using the rule above and starting with $13$, we generate the following sequence:
$$13 \rightarrow 40 \rightarrow 20 \rightarrow 10 \rightarrow 5 \rightarrow 16 \rightarrow 8 \rightarrow 4 \rightarrow 2 \rightarrow 1$$
It can be seen that this sequence (starting at $13$ and finishing at $1$) contains $10$ terms. Although it has not been proved yet (Collatz Problem), it is thought that all starting numbers finish at $1$.
Which starting number, under one million, produces the longest chain?
**NOTE:** Once the chain starts the terms are allowed to go above one million.

## 解决方案

直接将所有数的Collatz序列长度计算出来即可。

这里使用的一个技巧就是，可以把以前的计算结果记录下来。以后再次询问到相同的值可以直接进行返回，不需要再递归进行计算。

## 代码

```py
N = 10 ** 6
mp = {1: 1}


def dfs(u: int):
    if u in mp.keys():
        return mp[u]
    elif u & 1:
        mp[u] = dfs(u * 3 + 1) + 1
    else:
        mp[u] = dfs(u >> 1) + 1
    return mp[u]


ans, mx = 0, 0
for i in range(1, N):
    if dfs(i) > mx:
        mx = dfs(i)
        ans = i
print(ans)
```
