---
title: Project Euler 278
category:
  - Project Euler
tags:
mathjax: true
date: 2022-08-05 21:40:49
---

<escape><!-- more --></escape>

# Project Euler 278

## 题目

### Linear Combinations of Semiprimes

Given the values of integers $1 < a_1 < a_2 < \dots < a_n$, consider the linear combination

$q_1 a_1+q_2 a_2 + \dots + q_n a_n=b$, using only integer values $q_k \ge 0$.

Note that for a given set of $a_k$, it may be that not all values of $b$ are possible.

For instance, if $a_1=5$ and $a_2=7$, there are no $q_1 \ge 0$ and $q_2 \ge 0$ such that $b$ could be

$1, 2, 3, 4, 6, 8, 9, 11, 13, 16, 18$ or $23$.

In fact, $23$ is the largest impossible value of $b$ for $a_1=5$ and $a_2=7$.

We therefore call $f(5, 7) = 23$.

Similarly, it can be shown that $f(6, 10, 15)=29$ and $f(14, 22, 77) = 195$.

Find $\displaystyle \sum f( p\, q,p \, r, q \, r)$, where $p$, $q$ and $r$ are prime numbers and $p < q < r < 5000$.

## 解决方案

这篇[论文](https://www.emis.de/journals/INTEGERS/papers/g14/g14.pdf)给出了这种[硬币问题](https://en.wikipedia.org/wiki/Coin_problem)的一个特殊场景（定理$1$）：

假设序列$[a_1,a_2,\dots,a_k]$中的这些数**两两互质**，令$P=\prod_{i=1}^k a_i,A_i=\dfrac{P}{a_i},B=\sum_{i=1}^k A_i$。

那么有

$$f(A_1,A_2,\dots,A_k)=(k-1)P-B$$

回到本题。本题是这个结论$k=3$的情形，因此有：$f(pq,pr,qr)=2pqr-pq-pr-qr$

令$N=5000$以内的所有质数存放在下标为$0$的数组$pr$，其长度假设为$m$。并令其前缀和为$s$，满足$s[k]=\sum_{i=0}^k pr[i].$使用前缀和可以将上面的求和计算优化到$O(N)$的时间复杂度。枚举质数$q$，其为第$i$个质数$pr[i]$，那么左边的$p$和右边的$r$任意组合，可以计算出上式每一块的贡献值：

- $2pqr:2\cdot q \cdot(s[m-1]-s[i]) \cdot s[i-1]$
- $pr:(s[m-1]-s[i]) \cdot s[i-1]$
- $pq:s[i-1] \cdot q \cdot (m - 1 - i)$
- $qr:(s[m-1] - s[i]) \cdot q \cdot i$

注意前两块可以合并同类项。

## 代码

```py
from tools import get_prime

N = 5000
pr = get_prime(N)
s = []
for p in pr:
    s.append(p if len(s) == 0 else s[-1] + p)
m = len(pr)
ans = 0
for i in range(1, len(pr) - 1):
    q = pr[i]
    ans += (s[-1] - s[i]) * s[i - 1] * (q * 2 - 1) - s[i - 1] * q * (m - 1 - i) - (s[-1] - s[i]) * q * i

print(ans)

```
