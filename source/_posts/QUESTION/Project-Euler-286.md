---
title: Project Euler 286
tags:
  - Project Euler
  - 概率
  - 动态规划
  - 二分查找
mathjax: true
date: 2022-06-22 23:27:36
---

<escape><!-- more --></escape>

# Project Euler 286

## 题目

### Scoring probabilities

Barbara is a mathematician and a basketball player. She has found that the probability of scoring a point when shooting from a distance $x$ is exactly $(1-\dfrac{x}{q})$, where $q$ is a real constant greater than $50$.

During each practice run, she takes shots from distances $x=1, x=2, \dots, x=50$ and, according to her records, she has precisely a $2\%$ chance to score a total of exactly $20$ points.

Find $q$ and give your answer rounded to $10$ decimal places.

## 解决方案

令$N=50,M=20,Q=0.02$。如果$q$值确定了，那么可以使用动态规划的思想计算投篮$N$次，命中恰好$M$次的概率。

假设状态$f(i,j)(0\le i\le N,0\le j\le \min(i,M))$为已经投篮了$i$次，恰好命中了$j$次的概率，那么不难写出如下状态转移方程：

$$
f(i,j)=
\left \{\begin{aligned}
  &0  & & \mathrm{if\quad} i=0 \\
  &f(i-1,j)\cdot\dfrac{i}{q} & & \mathrm{else if\quad} j=0 \\
  &f(i-1,j-1)\cdot(1-\dfrac{i}{q}) & & \mathrm{else if\quad} j=i \\
  &f(i-1,j)\cdot\dfrac{i}{q} + f(i-1,j-1)\cdot(1-\dfrac{i}{q})& & \mathrm{else}
\end{aligned}\right.
$$

对于方程最后一行，前一项从$f(i-1,j)$时投篮不中转移过来，后一项则从$f(i-1,j-1)$时投篮命中转移过来。

当$q=50$时，发现$f(N,M)$约为$0.0412$，随着$q$的上升，发现$f(N,M)$下降得很快，因此考虑进行浮点数上的二分：如果$f(N,M)>Q$，那么说明$q$太小，否则$q$太大。

## 代码

```py
N = 50
M = 20
Q = 0.02
l = N
r = N << 1
for _ in range(100):
    q = 0.5 * (l + r)
    f = [[0 for i in range(M + 1)] for j in range(N + 1)]
    f[0][0] = 1
    for i in range(1, N + 1):
        rt = 1 - i / q
        for j in range(min(i, M) + 1):
            if j > 0:
                f[i][j] += f[i - 1][j - 1] * rt
            if j < i:
                f[i][j] += f[i - 1][j] * (1 - rt)
    if f[N][M] > Q:
        l = q
    else:
        r = q
ans = l
print("{:.10f}".format(ans))

```
