---
title: Project Euler 612
category:
  - Project Euler
tags:
  - 容斥原理
mathjax: true
date: 2022-08-05 21:41:52
---

<escape><!-- more --></escape>

# Project Euler 612

## 题目

### Friend numbers

Let's call two numbers  *friend numbers* if their representation in base $10$ has at least one common digit.

E.g. $1123$ and $3981$ are friend numbers.

Let $f(n)$ be the number of pairs $(p,q)$ with $1\le p \lt q \lt n$ such that $p$ and $q$ are friend numbers.

$f(100)=1539$.

Find $f(10^{18}) \mod 1000267129$.

## 解决方案

令$N=18$。考虑使用容斥原理完成。

用一个$10$位二进制数$d=d_9d_8\dots d_0$表示一个数$n$，$0,1,2,\dots9$中哪些数位出现了。如果$n$中有数位$i$，那么$d_i=1$，否则为$0$。

从$1$到$2^{10}-1$枚举这个十位二进制数$d$，假设$1(d)$为$d$这个数中$1$比特的个数。那么令$f(d)$表示$1\sim 10^{N}-1$这些数中，有多少个数，其所有数位使用的数都在$d$中表示为$1$（也就是说，就算$d_k=1$，这些数的数位中也不一定含有数位$k$）。那么有：

$$
f(d)=
\left \{\begin{aligned}
  &\sum_{n=1}^N (1(d))^n & & \mathrm{if\quad} d_0=0 \\
  &\sum_{n=1}^N (1(d))^{n-1} \cdot(1(d)-1) & & \mathrm{else}
\end{aligned}\right.
$$

这是因为，$0$不能放在最高位，而其他数字都可以任意填充。

接下来，令$g(d)$表示$1\sim 10^{N}-1$这些数中，有多少个数，其数位出现的情况表示为$d$（比$f$严格，$d_k=1$当且仅当数中含有数位$k$）。那么，通过容斥原理可以写出：

$$g(d)=\sum_{m\&d=m}(-1)^{1(d)-1(m)}f(m)$$

也就是说，一开始先将$f(d)$的全部情况记入$g(d)$，再将缺某一个数位的从$g(d)$减去，接下来再将缺两个数位的再加回去，因为多减了……

那么，只要将任意一对不含有相同数位的二元组减去，阿么剩下的都是友好数对。因此最终答案为：

$$\dfrac{(10^N-1)(10^N-2)}{2}-\sum_{i<j,i\&j=0} g(i)\cdot g(j)$$

## 代码

```py
N = 18
D = 10
mod = 1000267129

f = [0 for _ in range(1 << D)]
ones = [bin(i).count('1') for i in range(1 << D)]
for s in range(1, 1 << D):
    for i in range(1, N + 1):
        if s & 1:
            f[s] += (ones[s] - 1) * (ones[s] ** (i - 1))
        else:
            f[s] += ones[s] ** i
for s in range((1 << D) - 1, -1, -1):
    for k in range(s):
        if (k & s) == k:
            if (ones[s] - ones[k]) & 1:
                f[s] -= f[k]
            else:
                f[s] += f[k]
ans = (10 ** N - 1) * (10 ** N - 2) // 2
for i in range(1 << D):
    for j in range(i):
        if (i & j) == 0:
            ans -= f[i] * f[j]
ans %= mod
print(ans)

```
