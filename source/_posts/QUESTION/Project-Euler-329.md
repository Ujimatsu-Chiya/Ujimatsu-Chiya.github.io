---
title: Project Euler 329
tags:
  - Project Euler
  - 概率
  - 动态规划
mathjax: true
date: 2022-07-08 17:06:04
---

<escape><!-- more --></escape>

# Project Euler 329

## 题目

### Prime Frog

Susan has a prime frog.

Her frog is jumping around over $500$ squares numbered $1$ to $500$.

He can only jump one square to the left or to the right, with equal probability, and he cannot jump outside the range $[1;500]$. (if it lands at either end, it automatically jumps to the only available square on the next move.)

When he is on a square with a prime number on it, he croaks 'P' (PRIME) with probability $2/3$ or 'N' (NOT PRIME) with probability $1/3$ just before jumping to the next square.

When he is on a square with a number on it that is not a prime he croaks 'P' with probability $1/3$ or 'N' with probability $2/3$ just before jumping to the next square.

Given that the frog's starting position is random with the same probability for every square, and given that she listens to his first $15$ croaks, what is the probability that she hears the sequence PPPPNNPPPNPPNPN?

Give your answer as a fraction $p/q$ in reduced form.

## 解决方案

不难想到使用动态规划的方法来做。

令$M=500$，$s$是PPPPNNPPPNPPNPN这个字符串本身，下标从$0$开始，$N$是这个字符串的长度。本题需要注意的一点是，这只青蛙是先叫出字母，然后再进行移动。

假设$f(i,j)(0\le i\le N,1\le j\le M)$为青蛙已经**正确**地叫出了前$i$个字母，并且已经跳到了第$j$个格子的概率。那么不难写出如下状态转移方程：

$$
f(i,j)=
\left \{\begin{aligned}
  &\dfrac{1}{M}  & & \mathrm{if\quad} i=0 \\
  &f(i-1,j+1)\cdot q_M(j+1)\cdot p(j+1,s[i-1]) & & \mathrm{else if\quad} j=1 \\
  &f(i-1,j-1)\cdot q_M(j-1)\cdot p(j-1,s[i-1]) & & \mathrm{else if\quad} j=M \\
  &f(i-1,j+1)\cdot q_M(j+1)\cdot p(j+1,s[i-1])+f(i-1,j-1)\cdot q_M(j-1)\cdot p(j-1,s[i-1])& & \mathrm{else}
\end{aligned}\right.
$$

其中，$q_M(j)$表示如果$j$等于$1$或者是$M$，那么$q_M(j)=1$，否则$q_M(j)=\dfrac{1}{2}$；$p(n,c)$表示如果$n$的素性符合字母$c$的描述，那么$p(n,c)=\dfrac{2}{3}$，否则$p(n,c)=\dfrac{1}{3}$.

其中方程最后一行说明，第$j$个格子要么是从$j-1$以$q_M(j)$的概率跳过来的，并且有$p(j-1,s[i-1])$的概率叫出对应的字母；要么是从$j+1$跳过来的。

那么本题的最终答案为$\sum_{i=1}^M f(N,i)$。

为了方便代码编写，我这里使用的方法是“我为人人”式动态规划。

## 代码

```py
from fractions import Fraction
from tools import is_prime

M = 500
s = "PPPPNNPPPNPPNPN"
N = len(s)
f = [[Fraction(0, 1) for x in range(M + 1)] for y in range(N + 1)]
isp = [is_prime(i) for i in range(M + 1)]
f[0] = [Fraction(0)] + [Fraction(1, M)] * M
for i in range(N):
    for j in range(1, M + 1):
        q = 1 if j == 1 or j == M else Fraction(1, 2)
        p = Fraction(1, 3) if isp[j] ^ (s[i] == 'P') else Fraction(2, 3)
        if j < M:
            f[i + 1][j + 1] += f[i][j] * q * p
        if j > 1:
            f[i + 1][j - 1] += f[i][j] * q * p
ans = sum(f[N])
print(ans)

```
