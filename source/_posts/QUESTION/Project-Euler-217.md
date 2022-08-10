---
title: Project Euler 217
category:
  - Project Euler
tags:
  - 动态规划
mathjax: true
date: 2022-07-01 17:37:19
---

<escape><!-- more --></escape>

# Project Euler 217

## 题目

### Balanced Numbers

A positive integer with $k$ (decimal) digits is called balanced if its first $\left\lceil\dfrac{k}{2}\right\rceil$ digits sum to the same value as its last $\left\lceil\dfrac{k}{2}\right\rceil$ digits, where $\lceil x\rceil$, pronounced *ceiling* of $x$, is the smallest integer $\ge x$, thus $\lceil \pi\rceil=4$ and $\lceil 5\rceil=5$.

So, for example, all palindromes are balanced, as is $13722$.

Let $T(n)$ be the sum of all balanced numbers less than $10^n$. Thus: $T(1) = 45, T(2) = 540$ and $T(5) = 334795890$.
Find $T(47) \bmod 3^{15}$.

## 解决方案

令$N=47,M=\left\lfloor\dfrac{N}{2}\right\rfloor$。

由于数位的前一半位和后面一半位的和相等，那么我们首先通过动态规划的思想枚举一半数字中相同数字和下的所有数，然后再将它们重新组合起来即可。

那么，令状态$c(i,j)(1\le i\le M,0\le j\le 9i)$为**有**前导$0$的$i$位十进制数中，数位和为$j$的个数。那么不难写出以下状态转移方程：

$$
c(i,j)=
\left \{\begin{aligned}
  &1  & & \text{if}\quad i=1 \\
  &\sum_{k=0}^{\min(j,10)} c(i-1,j-k) & & \text{else}
\end{aligned}\right.
$$

其中，最后一行表示从一个数位和为$j-k$的$i-1$位数的最低位后面再添加一个数位$k$，那么就转移到了当前的状态。

令状态$s(i,j)(1\le i\le M,0\le j\le 9i)$为**有**前导$0$的$i$位十进制数中，数位和为$j$的所有数之和。那么可以写出以下状态转移方程：

$$
s(i,j)=
\left \{\begin{aligned}
  &1  & & \text{if}\quad i=1 \\
  &\sum_{k=0}^{\min(j,10)} 10 s(i-1,j-k)+k\cdot c(i-1)(j-k) & & \text{else}
\end{aligned}\right.
$$

其中，最后一行表示从一个数位和为$j-k$的$i-1$位数的最低位后面再添加一个数位$k$。这部分所有数都将乘以一个$10$再加到当前状态。然后还有最低位新添加的$k$，这一部分的数一共有$c(i-1,j-k)$个，因此当前状态还要补上$k\cdot c(i-1,j-k)$的和。

正式求解问题答案时，我们先枚举符合条件的数的数位个数$n$，令$m=\left\lfloor\dfrac{n}{2}\right\rfloor$，再枚举一半的数位和$d$。需要注意的是，组合的过程中，高一半位是**不能有**前导$0$，而低一半位是**可以有**前导$0$。而求不能有前导$0$的情况，只需要进行以下差分即可。也就是说，令$C(i,j)=c(i,j)-c(i-1,j),S(i,j)=s(i,j)-s(i-1,j)$。

1. 当$n$为偶数时，直接将前半部分的数直接和后半部分的数一一组合即可得。最终结果为$S(m,d)\cdot c(m,d)\cdot 10^m+s(m,d)\cdot C(m,d)$。
2. 当$n$为奇数时，注意到最中间的那个数位是可以任取的。那么，分成$3$部分来考虑这一些数的组合之和：左边一部分的数的组合之和为$S(m,d)\cdot c(m,d)\cdot 10^{m+1}\cdot 10$；中间的那个数位的组合之和$45\cdot 10^m\cdot C(m,d)\cdot c(m,d)$；右边一部分的组合之和为$s(m,d)\cdot C(m,d)\cdot 10$。将这三部分相加即可。

## 代码

```py
N = 47
mod = 3 ** 15
M = N >> 1
D = 9 * M
c = [[0 for _ in range(D + 1)] for _ in range(M + 1)]
s = [[0 for _ in range(D + 1)] for _ in range(M + 1)]
for j in range(10):
    c[1][j] = 1
    s[1][j] = j
for i in range(2, M + 1):
    for j in range(0, D + 1):
        for k in range(min(10, j + 1)):
            c[i][j] = (c[i][j] + c[i - 1][j - k]) % mod
            s[i][j] = (s[i][j] + 10 * s[i - 1][j - k] + k * c[i - 1][j - k]) % mod
ans = 45
for n in range(2, N + 1):
    m = n >> 1
    pw = pow(10, m, mod)
    for d in range(1, 9 * m + 1):
        cl, cr = c[m][d] - c[m - 1][d], c[m][d]
        sl, sr = s[m][d] - s[m - 1][d], s[m][d]
        if n % 2 == 0:
            ans = (ans + sl * cr * pw + sr * cl) % mod
        else:
            ans = (ans + sl * cr * pw * 10 * 10 + 45 * pw * cl * cr + sr * cl * 10) % mod
print(ans)

```
