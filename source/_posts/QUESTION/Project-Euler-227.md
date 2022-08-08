---
title: Project Euler 227
category:
  - Project Euler
tags:
  - 概率
  - 动态规划
mathjax: true
date: 2022-07-01 17:36:51
---

<escape><!-- more --></escape>

# Project Euler 227

## 题目

### The Chase

*The Chase* is a game played with two dice and an even number of players.

The players sit around a table; the game begins with two opposite players having one die each. On each turn, the two players with a die roll it.

If a player rolls a $1$, he passes the die to his neighbour on the left; if he rolls a $6$, he passes the die to his neighbour on the right; otherwise, he keeps the die for the next turn.

The game ends when one player has both dice after they have been rolled and passed; that player has then lost.

In a game with $100$ players, what is the expected number of turns the game lasts?

Give your answer rounded to ten significant digits.

## 解决方案

令$N=100$，注意$N$必须是偶数，并令$M=\dfrac{N}{2}$。不难发现，当前游戏的状态并不取决于是哪两个人拿着骰子，而只取决于拿着骰子的两个人的距离（注意这个距离是指比较短的那段距离，也就是两个人在圆上的**劣弧**长度）。

那么，令$d_N(x)=\min(x\%N,(-x)\%N)$，其中$x$是两人在优弧或者劣弧上的距离，$d_N(x)$用于求出两人在劣弧上的距离。

根据题意，两人同时抛骰子，那么两个人距离的**变化值**的分布律可以写出：

|$d$|$-2$|$-1$|$0$|$1$|$2$|
|-|-|-|-|-|-|
|$p(d)$|$\dfrac{1}{36}$|$\dfrac{2}{9}$|$\dfrac{1}{2}$|$\dfrac{2}{9}$|$\dfrac{1}{36}$|

那么，令状态$f(i)(0\le i\le M)$表示从游戏一开始后，两个骰子之间的距离第一次达到$i$的期望游戏轮数。对于$\forall i,0\le i< M$，可以写出：

$$f(i)=1+\sum_{d=-2}^2f(d_N(i+d))\cdot p(d)\qquad(1)$$

由于游戏的初始状态是$M$，因此$f(M)=0$。

这是一个**有后效性**的动态规划方程，因为状态之间形成了循环的依赖（状态$i$依赖于自身）。不过，这种情况下消除后效性很简单。右边有一个项也是$f(i)$，只需要挪到左边消除就可以完成消除后效性，从而正确计算结果。

那么，将$f$中的每一个值全部当成是未知数，那么方程$(1)$和$f(M)=0$构成了一个$M+1$元的线性方程组，解这个方程组即可，最终$f(0)$即为答案。

## 代码

```py
import numpy as np

N = 100
con = [1, 8, -18, 8, 1]
M = N >> 1
b = [-36] * M + [0]
a = []
for i in range(M):
    t = [0 for _ in range(M + 1)]
    for j in range(5):
        x = i + j - 2
        t[min(x % N, -x % N)] += con[j]
    a.append(t)
a.append([0] * M + [1])
x = np.linalg.solve(a, b)
ans = x[0]
print("{:.6f}".format(ans))

```
