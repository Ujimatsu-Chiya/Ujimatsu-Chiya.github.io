---
title: Project Euler 260
tags:
  - Project Euler
  - 博弈论
mathjax: true
date: 2022-07-04 18:03:39
---

<escape><!-- more --></escape>

# Project Euler 260

## 题目

### Stone Game

A game is played with three piles of stones and two players.

At her turn, a player removes one or more stones from the piles. However, if she takes stones from more than one pile, she must remove the same number of stones from each of the selected piles.
In other words, the player chooses some $N>0$ and removes:

- $N$ stones from any single pile; or
- $N$ stones from each of any two piles ($2N$ total); or
- $N$ stones from each of the three piles ($3N$ total).

The player taking the last stone(s) wins the game.
A *winning configuration* is one where the first player can force a win.For example, $(0,0,13), (0,11,11)$ and $(5,5,5)$ are winning configurations because the first player can immediately remove all stones.

A *losing configuration* is one where the second player can force a win, no matter what the first player does.For example, $(0,1,2)$ and $(1,3,3)$ are losing configurations: any legal move leaves a winning configuration for the second player.

Consider all losing configurations $(x_i,y_i,z_i)$ where $x_i \le y_i \le z_i \le 100$.We can verify that $\sum(x_i+y_i+z_i) = 173895$ for these.

Find $\sum(x_i+y_i+z_i)$ where $(x_i,y_i,z_i)$ ranges over the losing configurations with $x_i \le y_i \le z_i \le 1000$.

## 解决方案

令$N=1000$。这是一个[无偏博弈](https://en.wikipedia.org/wiki/Impartial_game)，我们可以将游戏的状态视为有向无环图上的一个个节点。

1. 一个状态是必败状态，当且仅当它的所有后继的状态都是必胜状态。
2. 一个状态是必败状态，当且仅当它存在一个后继的状态是必败状态。
3. 由于取完所有石头就是胜利，因此没有后继的状态$(0,0,0)$是必败状态。

那么，对于一个状态$(x,y,z)$，它有以下这么多种后继状态：

$\begin{aligned}
& (x-s,y,z),1\le s\le x\\
& (x,y-s,z),1\le s\le y\\
& (x,y,z-s),1\le s\le z\\
& (x,y-s,z-s),1\le s\le \min(y,z)\\
& (x-s,y,z-s),1\le s\le \min(x,z)\\
& (x-s,y-s,z),1\le s\le \min(x,y)\\
& (x-s,y-s,z-s),1\le s\le \min(x,y,z)\\
\end{aligned}$

那么，当我们考虑一个状态$(x,y,z)$的类型时，需要线性的时间复杂度。程序总体时间复杂度为$O(N^4)$，这明显是不能接受的。

我们尝试将上面的每一种后继状态“集合”起来。然后分别判断整个集合里面是否都是存放的必胜态。

有一些状态的分量因为大家都减去了$s$，但是其之间相对的差值仍然不会改变，考虑使用这些不变的相对差值将状态集中起来，那么可以如下集中：

$\begin{aligned}
& (x-s,y,z)\rightarrow s_1(y,z)\\
& (x,y-s,z)\rightarrow s_1(x,z)\\
& (x,y,z-s)\rightarrow s_1(x,y)\\
& (x,y-s,z-s)\rightarrow s_2(x,z-y)\\
& (x-s,y,z-s)\rightarrow s_2(y,z-x)\\
& (x-s,y-s,z)\rightarrow s_2(z,y-x)\\
& (x-s,y-s,z-s)\rightarrow s_3(y-x,z-y)\\
\end{aligned}$

在判断状态$(x,y,z)$的类型时，只需要以常数时间维护好这些$s$值，然后就能够以常数时间判断。最终时间复杂度为$O(N^3)$。

## 代码

```C++
#include <bits/stdc++.h>
typedef long long ll;
const int N = 1000;
bool s1[N + 1][N + 1];
bool s2[N + 1][N + 1];
bool s3[N + 1][N + 1];
int main() {
    ll ans=0;
    for (int x = 0; x <= N; x++)
        for (int y = x; y <= N; y++)
            for (int z = y; z <= N; z++) {
                if (!(s3[y - x][z - y] || s2[z][y - x] || s2[y][z - x] || s2[x][z - y] || s1[y][z] || s1[x][z] || s1[x][y])) {
                    s3[y - x][z - y] = true;
                    s2[z][y - x] = true;
                    s2[y][z - x] = true;
                    s2[x][z - y] = true;
                    s1[x][y] = true;
                    s1[x][z] = true;
                    s1[y][z] = true;
                    ans += x + y + z;
                }
            }
    printf("%lld\n", ans);
}

```
