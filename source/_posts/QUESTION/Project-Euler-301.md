---
title: Project Euler 301
tags:
  - Project Euler
  - 博弈论
  - 动态规划
mathjax: true
date: 2022-07-06 13:08:24
---

<escape><!-- more --></escape>

# Project Euler 301

## 题目

### Nim

*Nim* is a game played with heaps of stones, where two players take it in turn to remove any number of stones from any heap until no stones remain.
We’ll consider the three-heap normal-play version of Nim, which works as follows:

- At the start of the game there are three heaps of stones.
- On his turn the player removes any positive number of stones from any single heap.
- The first player unable to move (because no stones remain) loses.

If $(n_1,n_2,n_3)$ indicates a Nim position consisting of heaps of size $n_1, n_2$ and $n_3$ then there is a simple function $X(n_1,n_2,n_3)$ — that you may look up or attempt to deduce for yourself — that returns:

- zero if, with perfect strategy, the player about to move will eventually lose; or
- non-zero if, with perfect strategy, the player about to move will eventually win.

For example $X(1,2,3) = 0$ because, no matter what the current player does, his opponent can respond with a move that leaves two heaps of equal size, at which point every move by the current player can be mirrored by his opponent until no stones remain; so the current player loses. To illustrate:

- current player moves to $(1,2,1)$
- opponent moves to $(1,0,1)$
- current player moves to $(0,0,1)$
- opponent moves to $(0,0,0)$, and so wins.

For how many positive integers $n\le2^{30}$ does $X(n,2n,3n) = 0$?

## 解决方案

关于这个[NIM](https://en.wikipedia.org/wiki/Nim#Mathematical_theory)博弈的页面，给出了一个更一般的方法用来判断当前游戏状态是必胜态还是必败态：

假设一共有$n$堆石头，每一堆的个数为$a_i$。那么游戏是必败态时，当且仅当

$$\bigoplus_{i=1}^n a_i=a_1\oplus a_2\oplus a_3 \oplus\dots\oplus a_n=0$$

其中$\oplus$是异或运算。

因此，问题转化成有多少个正整数$n\le 2^{N},N=30$，满足$n\oplus 2n\oplus 3n=0$.也就是$n\oplus 2n= 3n$.

异或运算也被视为是二进制下的不进位加法。因此，当$n$和$2n$没有重合的$1$比特，也就是$n\&2n=0$时，才会满足$n\oplus2n=n+2n=3n$相等。否则，因为异或中进位被消除了，那么$n\oplus 2n<3n$.

当$n\&2n=0$时，$n$不允许有两个相邻的位为$1$.将$n=2^N$对应到$n=0$时的情况。那么问题就变成了有多少个$N$比特数，其中不存在两个相邻的位同为$1$？假设这个值为$F(N)$，那么不难发现这通过动态规划的思想就可以做出来：

$f(1)=2,f(2)=3,f(i)=f(i-2)+f(i-1)$

此处不再详述这个动态规划的过程。另外这道题的答案其实是斐波那契数。

## 代码

```py
N = 30
f = [1, 2]
for i in range(N):
    f.append(f[-1] + f[-2])
print(f[N])

```
