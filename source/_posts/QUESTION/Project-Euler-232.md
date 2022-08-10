---
title: Project Euler 232
category:
  - Project Euler
tags:
  - 概率
  - 动态规划
mathjax: true
date: 2022-07-01 17:36:55
---

<escape><!-- more --></escape>

# Project Euler 232

## 题目

### The Race

Two players share an unbiased coin and take it in turns to play *The Race*.

On Player $1$'s turn, the coin is tossed once. If it comes up Heads, then Player $1$ scores one point; if it comes up Tails, then no points are scored.

On Player $2$'s turn, a positive integer, $T$, is chosen by Player $2$ and the coin is tossed $T$ times. If it comes up all Heads, then Player $2$ scores $2^{T-1}$ points; otherwise, no points are scored.

Player $1$ goes first and the winner is the first to $100$ or more points.

Player $2$ will always selects the number, $T$, of coin tosses that maximises the probability of winning.

What is the probability that Player $2$ wins?

Give your answer rounded to eight decimal places in the form $0.abcdefgh$.

## 解决方案

不难想到可以使用动态规划的思想解决。

令$N=100$。令状态$f(i,j)(0\le i,j\le N)$表示当前是**玩家**$\mathbf{2}$的回合，玩家$1$**仍需要**获得$i$分，玩家$2$**仍需要**获得$j$分的情况下，玩家$2$的胜率。

假设$w_1=0.5,l_1=0.5$分别是玩家$1$单个回合的成功率和失败率，$w_2(T)=2^{T},l_2(T)=1-2^{T}$对玩家$2$同理。令$g(j,T)=\max(j-2^{T-1},0)$，那么对$f(i,j)$的其中一个决策$T$可以写出如下方程：

$\begin{aligned}
f(i,j)=&w_1\cdot w_2(T)\cdot f(i-1,g(j,T))+l_1\cdot w_2(T)\cdot f(i,g(j,T))+\\
&w_1\cdot l_2(T)\cdot f(i-1,j) + l_1\cdot l_2(T)\cdot f(i,j)
\end{aligned}$

这个方程表示玩家$2$先玩，接下来玩家$1$玩，两人分别成功和失败的组合，一共有四对。

这是一个**有后效性**的动态规划方程，因为状态之间形成了循环的依赖（状态$(i,j)$依赖于自身）。不过，这种情况下消除后效性很简单。右边有一个项也是$f(i,j)$，只需要挪到左边消除就可以完成消除后效性，从而正确计算结果。

因此，可以正式地写出$f(i,j)$的状态转移方程：

$$
f(i,j)=
\left \{\begin{aligned}
  &1 & & \text{if\quad} j=0 \\
  &0 & & \text{else if\quad} i=0 \\
  &\max_{2^{T-2}\le j}\{\dfrac{w_1\cdot w_2(T)\cdot f(i-1,g(j,T))+l_1\cdot w_2(T)\cdot f(i,g(j,T))+w_1\cdot l_2(T)\cdot f(i-1,j)}{1-l_1\cdot l_2(T)}\} & & \text{else}
\end{aligned}\right.
$$

需要注意的是，$(0,0)$本身不是一个合法的状态，但是为了方便计算故列出。因为玩家$2$在他自己的回合已经胜出游戏，因此$f(0,0)=1$。

由于这个游戏是一开始是玩家$1$的回合，玩家$2$的胜率是以玩家$1$的回合结束**作为条件**的。因此玩家$2$在整场游戏的胜率为$w_1\cdot f(N-1,N)+l_1\cdot f(N,N)$.

## 代码

```py
N = 100
w1 = l1 = 0.5
f = [[0 for _ in range(N + 1)] for _ in range(N + 1)]
for i in range(N + 1):
    for j in range(N + 1):
        if j == 0:
            f[i][j] = 1
        elif i == 0:
            f[i][j] = 0
        else:
            pw = 1
            while True:
                w2 = 0.5 / pw
                l2 = 1.0 - w2
                t = max(j - pw, 0)
                nw = w1 * w2 * f[i - 1][t] + l1 * w2 * f[i][t] + w1 * l2 * f[i - 1][j]
                nw /= 1 - l1 * l2
                f[i][j] = max(f[i][j], nw)
                if t == 0:
                    break
                pw <<= 1
ans = l1 * f[N][N] + w1 * f[N - 1][N]
print("{:.8f}".format(ans))

```
