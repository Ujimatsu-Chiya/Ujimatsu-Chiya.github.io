---
title: Project Euler 692
category:
  - Project Euler
tags:
  - 博弈论
  - 齐肯多夫定理
mathjax: true
date: 2022-07-17 23:11:29
---

<escape><!-- more --></escape>

# Project Euler 692

## 题目

### Siegbert and Jo

Siegbert and Jo take turns playing a game with a heap of $N$ pebbles:

1. Siegbert is the first to take some pebbles. He can take as many pebbles as he wants. (Between $1$ and $N$ inclusive.)
2. In each of the following turns the current player must take at least one pebble and at most twice the amount of pebbles taken by the previous player.
3. The player who takes the last pebble wins.

Although Siegbert can always win by taking all the pebbles on his first turn, to make the game more interesting he chooses to take the smallest number of pebbles that guarantees he will still win (assuming both Siegbert and Jo play optimally for the rest of the game).

Let $H(N)$ be that minimal amount for a heap of $N$ pebbles.

$H(1)=1$, $H(4)=1$, $H(17)=1$, $H(8)=8$ and $H(18)=5$ .

Let $G(n)$ be $\displaystyle{\sum_{k=1}^n H(k)}$.

$G(13)=43$.

Find $G(23416728348467685)$.

## 解决方案

这个游戏是[斐波那契Nim](https://en.wikipedia.org/wiki/Fibonacci_nim)，页面说明了$H(n)$是$n$的[齐肯多夫表示法](https://en.wikipedia.org/wiki/Zeckendorf%27s_theorem)中的最小项。

将$H(n)$的前一部分项打印出来，并在OEIS上查找到为[A139764](https://oeis.org/A139764)。

假设$f(n)$是小于等于$n$以内的最大斐波那契数。观察$H(n)$的特征，发现：

- 如果$n$是斐波那契数，那么$H(n)=f(n)$
- 如果$n$不是斐波那契数，那么$H$的第$f(n)+1$项到第$n$项这一段，和第$1$项到$n-f(n)$这一段是完全相同的。

因此不难计给出计算$G(n)$的递推式：

$$
G(n)=
\left \{\begin{aligned}
  &1 & & \text{if}\quad  n=1 \\
  &G(n-1)+n  & & \text{else if}\quad  f(n)=n \\
  &G(n-f(n))+G(f(n))& & \text{else}
\end{aligned}\right.
$$

采用记忆化的方式，那么可以在$O(\log n)$的时间复杂度内完成计算。

## 代码

```py
N = 23416728348467685
f = [1, 2]
while True:
    f.append(f[-1] + f[-2])
    if f[-1] > N:
        break
G = {1: 1}


def getG(n: int):
    if n in G.keys():
        return G[n]
    for p in range(len(f) - 1):
        if f[p + 1] > n:
            break
    if f[p] == n:
        G[n] = getG(n - 1) + n
    else:
        G[n] = getG(f[p]) + getG(n - f[p])
    return G[n]


ans = getG(N)
print(ans)

```
