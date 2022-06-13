---
title: Project Euler 684
tags:
  - Project Euler
  - 贪心
mathjax: true
date: 2022-06-13 21:21:42
---

<escape><!-- more --></escape>

# Project Euler 684

## 题目

### Inverse Digit Sum

Define $s(n)$ to be the smallest number that has a digit sum of $n$. For example $s(10) = 19$.

Let $\displaystyle S(k) = \sum_{n=1}^k s(n)$. You are given $S(20) = 1074$.

Further let $f_i$ be the Fibonacci sequence defined by $f_0=0, f_1=1$ and $f_i=f_{i-2}+f_{i-1}$ for all $i \ge 2$.

Find $\displaystyle \sum_{i=2}^{90} S(f_i)$. Give your answer modulo $1\,000\,000\,007$.

## 解决方案

基于贪心思想，$s(n)$中除了最高位以外，其它位全是$9$。因此，$s(n)$的值为如下形式：$?999999999\dots$这样保证了$s(n)$的位数是最小的，并且分配给高位的数是尽量小的。因此，$s(n)=10^{\lfloor\frac{n}{9}\rfloor}\cdot(n\%9+1)-1$。

$s(n)$中从小到大，每$9$个数划分成一块，那么不难发现，每一块里面的数都是$1999\dots$到$9999\dots$，每一块的长度完全一样。

令$n=9q+r,0\le r<9$，那么$S(n)$由以下两部分数组成：

1. 所有完整的块的数字之和，这一部分数字有$q$个完整的块，这些完整的块的数之和通过等比数列公式容易求出为$6\times(10^q-1)-9q$.

2. 最后一块不完整的数之和这些数之和。这些数一共有$r$个，都是$k+1$位数。它们的和为$\dfrac{1}{2}r(10^q(r+3)-2)$

两部分加起来，得到:

$$S(n) = \left(\frac{(r+2)(r+1)}{2} + 5\right)\cdot 10^q-9q-6-r$$

## 代码

```py
N = 90
mod = 10 ** 9 + 7
f = [0, 1]
for i in range(2, N + 1):
    f.append(f[-1] + f[-2])
ans = 0
for w in f[2:]:
    q, r = divmod(w, 9)
    ans = (ans + ((r + 1) * (r + 2) // 2 + 5) * pow(10, q, mod) - 9 * q - 6 - r) % mod
print(ans)

```
