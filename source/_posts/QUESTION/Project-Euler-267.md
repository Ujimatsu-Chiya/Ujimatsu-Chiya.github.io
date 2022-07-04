---
title: Project Euler 267
tags:
  - Project Euler
mathjax: true
date: 2022-07-04 18:02:13
---

<escape><!-- more --></escape>

# Project Euler 267

## 题目

### Billionaire

You are given a unique investment opportunity.

Starting with $£1$ of capital, you can choose a fixed proportion, $f$, of your capital to bet on a fair coin toss repeatedly for $1000$ tosses.

Your return is double your bet for heads and you lose your bet for tails.

For example, if $f=\dfrac{1}{4}$,  for the first toss you bet $£0.25$, and if heads comes up you win $£0.5$ and so then have $£1.5$. You then bet $£0.375$ and if the second toss is tails, you have $£1.125$.

Choosing $f$ to maximize your chances of having at least $£1,000,000,000$ after $1,000$ flips, what is the chance that you become a billionaire?

All computations are assumed to be exact (no rounding), but give your answer rounded to $12$ digits behind the decimal point in the form 0.abcdefghijkl.

## 解决方案

令$N=1000,M=10^9$.根据题意，选定了$f$后抛一次硬币，如果正面向上，那么资本变成原来的$(1+2f)$倍，否则变成原来的$(1-f)$倍。

那么，如果在整个过程中有$n$次硬币正面在上，那么最终获得的金额数是：

$$P(n)=(1+2f)^n\cdot(1-f)^{N-n}$$

不难发现，随着$n$增长，$P(n)$也在增长，那么存在一个最小的$n=n_0$使得$P(n_0)\ge M$。因此题目就转化成：求值$f$，使得这个$n_0$能够最小。

对不等式两边取对数，可以写成：$n\log(1+2f)+(N-n)\log(1-f)\ge \log M$

经过移项，那么可以写成$n(\log(1+2f)-\log(1-f))+N\log(1-f)\ge \log M$

由于$f>0$，因此移项后就写成$n\ge\dfrac{\log M-N\log(1-f)}{\log(1+2f)-\log(1-f)}$

令函数$h(x)=\dfrac{\log M-N\log(1-x)}{\log(1+2x)-\log(1-x)},0< x<1$.那么此时就是为了求函数$h(x)$的最小值。这里使用scipy.optimize中的fminbound方法求函数$h$的极小值点$x_0$。

那么，最小的$n_0$就满足$n_0=\lceil h(x_0)\rceil$。

根据二项分布的性质，不难得出最终结果为$\dfrac{\sum_{i=n_0}^N C_N^i}{2^N}$.

## 代码

```py
from math import log2, ceil
from scipy.optimize import fminbound
from tools import get_pascals_triangle

N = 1000
M = 10 ** 9
h = lambda x: (log2(M) - N * log2(1 - x)) / (log2(1 + 2 * x) - log2(1 - x))
f = fminbound(h, 0, 1)
n0 = ceil(h(f))
C = get_pascals_triangle(N)
ans = sum(C[N][j] for j in range(n0, N + 1)) / (1 << N)
print("{:.12f}".format(ans))

```
