---
title: Project Euler 253
category:
  - Project Euler
tags:
  - 动态规划
mathjax: true
date: 2022-07-04 18:02:46
---

<escape><!-- more --></escape>

# Project Euler 253

## 题目

### Tidying up

A small child has a “number caterpillar” consisting of forty jigsaw pieces, each with one number on it, which, when connected together in a line, reveal the numbers $1$ to $40$ in order.

Every night, the child’s father has to pick up the pieces of the caterpillar that have been scattered across the play room. He picks up the pieces at random and places them in the correct order. As the caterpillar is built up in this way, it forms distinct segments that gradually merge together. The number of segments starts at zero (no pieces placed), generally increases up to about eleven or twelve, then tends to drop again before finishing at a single segment (all pieces placed).

For example:

|**Piece Placed**|**Segments So Far**|
|-|-|
|$12$|$1$|
|$4$|$2$|
|$29$|$3$|
|$6$|$4$|
|$34$|$5$|
|$5$|$4$|
|$35$|$4$|
|$\dots$|$\dots$|

Let $M$ be the maximum number of segments encountered during a random tidy-up of the caterpillar.

For a caterpillar of ten pieces, the number of possibilities for each $M$ is

|**M**|**Possibilities**|
|-|-|
|$1$|$512$|
|$2$|$250912$|
|$3$|$1815264$|
|$4$|$1418112$|
|$5$|$144000$|

so the most likely value of $M$ is $3$ and the average value is $\dfrac{385643}{113400} = 3.400732$, rounded to six decimal places.
The most likely value of $M$ for a forty-piece caterpillar is $11$; but what is the average value of $M$?

Give your answer rounded to six decimal places.

## 解决方案

本题使用动态规划的思想解决。

令$N=40,M=\lceil\dfrac{M+1}{2}\rceil$。假设$f(i,j,k)(0< k\le M)$表示已经放置了$i$件拼图，并已经形成了$j$个连续的段，并在放置的过程中，段数不超过$k$的放法。那么状态转移方程就可以写作：

$$
f(i,j,k)=
\left \{\begin{aligned}
  &1 & & \mathrm{if\quad} i=1,j=1 \\
  &0 & & \mathrm{else if\quad} i=1|j\le 0| j> k \\
  &j\cdot f(i-1,j-1,k)+j\cdot f(i-1,j+1,k)+2j\cdot f(i-1,j,k)& & \mathrm{else}
\end{aligned}\right.
$$

对于方程的最后一行，状态$f(i-1,j-1,k)$中有$j-1$个不同的段，那么我们拥有$s$个位置放置一块拼图形成一个新的段；状态$f(i-1,j+1,k)$中有$j+1$个段，那么我们有$j$个位置把相邻的两个段通过一个拼图形成一个新的段；状态$f(i-1,j,s)$中的每个段，直接在左边或者右边延伸，那么就有$2s$种延伸方式。

那么，最终答案为：

$$\dfrac{\sum_{i=1}^M i\cdot(f(N,1,i)-f(N,1,i-1))}{N!}$$

## 代码

```py
from tools import fac

N = 40
M = (N + 1) >> 1
mp = {}


def f(n, m, p):
    if n == 1:
        return int(m == 1)
    elif m <= 0 or m > p:
        return 0
    if (n, m, p) not in mp.keys():
        mp[n, m, p] = f(n - 1, m - 1, p) * m + f(n - 1, m + 1, p) * m + f(n - 1, m, p) * m * 2
    return mp[n, m, p]


ans = sum(i * (f(N, 1, i) - f(N, 1, i - 1)) for i in range(1, M + 1)) / fac(N)
print("{:.6f}".format(ans))

```
