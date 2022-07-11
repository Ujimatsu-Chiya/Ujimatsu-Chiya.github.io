---
title: Project Euler 443
tags:
  - Project Euler
mathjax: true
date: 2022-07-12 00:17:23
---

<escape><!-- more --></escape>

# Project Euler 443

## 题目

### GCD sequence

Let $g(n)$ be a sequence defined as follows:

$g(4) = 13$,

$g(n) = g(n-1) + \gcd(n, g(n-1))$, for $n > 4$.

The first few values are:

||||||||||||||||||||
|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|
|$n$|$4$|$5$|$6$|$7$|$8$|$9$|$10$|$11$|$12$|$13$|$14$|$15$|$16$|$17$|$18$|$19$|$20$|$\dots$|
|$g(n)$|$13$|$14$|$16$|$17$|$18$|$27$|$28$|$29$|$30$|$31$|$32$|$33$|$34$|$51$|$54$|$55$|$60$|$\dots$|

You are given that $g(1000) = 2524$ and $g(1000000) = 2624152$.

Find $g(10^{15})$.

## 解决方案

令$N=10^{15}$，将$g$中的前一部分项打印出来，发现对于绝大多数$n$，都满足$g(n)=g(n-1)+1$。

因此，我们考虑枚举出所有满足$\gcd(n,g(n-1))>1$的所有$n$，并找到这些$n$中最大的一个使得$n\le N$，那么$g(N)=g(n)+N-n.$

假设目前我们已经知道了某个$n$和它的函数值$g$，那么转为求下一个最小的$n'$使得$\gcd(n',g(n'-1))>1,n'>n$，那么在$d=n+1,n+2,\dots,n'-1$之前，都满足$\gcd(d,g(d-1))=1$。

那么对于一对$n,g$，问题转化成求一个最小的$k$，使得$\gcd(n+k+1,g+k)>1$.根据辗转相除的性质，可以写为$\gcd(g+k,g-n-1)>1$.

可以发现，$g-n-1$是一个常数。因此我们将$g-n-1$进行分解，并枚举每个质因数$p_i$，并求出最小的$k_i$使得$g+k_i$是$p_i$的倍数，最终$k$是这些$k_i$中最小的一个。

令$n'=n+k+1$，那么$g'=n+k+\gcd(n+k+1,g+k)$，得到了一组新的$n',g(n)$值，由此迭代直到$N$处。

## 代码

```py
from tools import factorization, gcd

N = 10 ** 15
n = 4
g = 13
while True:
    p_list = [u[0] for u in factorization(g - n - 1)]
    nxt = min((g + p - 1) // p * p for p in p_list)
    k = nxt - g
    np = n + k + 1
    if np > N:
        g += N - n
        break
    g = nxt + gcd(np, nxt)
    n = np
print(g)

```
