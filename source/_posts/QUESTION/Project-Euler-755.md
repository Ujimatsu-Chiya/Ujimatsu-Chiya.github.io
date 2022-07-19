---
title: Project Euler 755
tags:
  - Project Euler
  - 动态规划
mathjax: true
date: 2022-07-19 00:28:44
---

<escape><!-- more --></escape>

# Project Euler 755

## 题目

### Not Zeckendorf

Consider the Fibonacci sequence $\{1,2,3,5,8,13,21,\ldots\}$.

We let $f(n)$ be the number of ways of representing an integer $n\ge 0$ as the sum of different Fibonacci numbers.

For example, $16 = 3+13 = 1+2+13 = 3+5+8 = 1+2+5+8$ and hence $f(16) = 4$.
By convention $f(0) = 1$.

Further we define
$$\displaystyle S(n) = \sum_{k=0}^n f(k)$$
You are given $S(100) = 415$ and $S(10^4) = 312807$.

Find $\displaystyle S(10^{13})$.

## 解决方案

令$N=10^{13}$。假设题目中提到的斐波那契数列为$F$，下标从$1$开始。

我们考虑一个斐波那契数集合中所有数的构成方案数。考虑使用动态规划的思想进行。令状态$f(k,s)(k\ge 0)$表示由$F$中的前$k$个数组成的集合中，能够选择多少个不同的子集，使得自己的元素和小于等于$s$.那么可以写出$f$的状态转移方程：

$$
f(k,s)=
\left \{\begin{aligned}
  &0  & & \mathrm{if\quad} s<0 \\
  &1 & & \mathrm{else if\quad} k=0 \\
  &2^k & & \mathrm{else if\quad} \sum_{i=1}^k F_i\le N \\
  &f(k-1,s)+f(k-1,s-F_k) & & \mathrm{else}
\end{aligned}\right.
$$

方程的倒数第二行说明，如果整个集合的元素和都不超过$s$，那么无论怎么选都可以，一共有$2^k$种选法。方程的最后一行$f(k-1,s)$说明$F_k$不被选取，进入到下一轮；$f(k-1,s-F_k)$则说明$F_k$被选取了，与此同时$1\sim F_k-1$的拼接方法将不再考虑。

那么最终答案为$S(N)=f(t,N)$，其中$t$是满足$F_t\ge N$的最小值。

如果添加上记忆化，那么求解$f$的效率将会很高。

## 代码

```py
N = 10 ** 13
f = [1, 2]
while True:
    w = f[-1] + f[-2]
    if w > N:
        break
    f.append(w)
s = [sum(f[:i + 1]) for i in range(len(f))]
mp = {}


def dfs(fl: int, now: int):
    if now < 0:
        return 0
    if fl == 0:
        return 1
    elif s[fl - 1] <= now:
        return 1 << fl
    else:
        if (fl, now) not in mp.keys():
            mp[fl, now] = dfs(fl - 1, now) + dfs(fl - 1, now - f[fl - 1])
        return mp[fl, now]


print(dfs(len(f), N))

```
