---
title: Project Euler 70
category:
  - Project Euler
tags:
mathjax: true
date: 2022-04-30 10:32:32
---

<escape><!-- more --></escape>

# Project Euler 70

## 题目

### Totient permutation

Euler’s Totient function, $\varphi(n)$ [sometimes called the phi function], is used to determine the number of numbers less than $n$ which are relatively prime to $n$. For example, as $1, 2, 4, 5, 7,$ and $8$, are all less than nine and relatively prime to nine, $\varphi(9)=6$.

The number $1$ is considered to be relatively prime to every positive number, so $\varphi(1)=1$.

Interestingly, $\varphi(87109)=79180$, and it can be seen that $87109$ is a permutation of $79180$.

Find the value of $n, 1 < n < 10^7$, for which $\varphi(n)$ is a permutation of $n$ and the ratio $n/\varphi(n)$ produces a minimum.

## 解决方案

需要注意，本题是求得满足排列要求的，并且使$\dfrac{n}{\varphi(n)}$最小的，在范围$n<N$内的一个$n$。

根据欧拉函数的公式$\varphi(n)=n\prod(1-\dfrac{1}{p_i})$，可以知道，这个比值就等于$\prod \dfrac{p_i}{p_i-1}$.

根据这个式子可以发现，只需要考虑质因数质数不大于$1$的情况即可，因为这个式子的大小和$e_i$没有任何关系。

单独讨论一个质数$p$。很明显的是，随着$p$的增长，$\dfrac{p}{p-1}$值逐渐减小。这说明，求出的$n$的质因数都应该是尽可能大的。

因此，有另外一个推论：$n$的质因数个数越少越好。

先考虑只有一个质因数的情况，也就是质数$p$。但是,$\varphi(p)=p-1$，$p-1$不可能是$p$的一个排列。

故考虑两个质因数的情况。枚举所有比较接近$\sqrt N$的质数，将它们两两相乘，得到一些列形如$p_ip_j$，其中$p_ip_j\leq N$的数，直接筛选。

## 代码

```py
from gmpy2 import isqrt
from tools import get_prime

N = 10 ** 7
M = isqrt(N)
pr = get_prime(M // 5, M * 5 - 1)
val = 100
for i in range(len(pr)):
    for j in range(i + 1, len(pr)):
        w = pr[i] * pr[j]
        if w >= N:
            break
        phi = (pr[i] - 1) * (pr[j] - 1)
        if "".join((lambda x: (x.sort(), x)[1])(list(str(w)))) == \
                "".join((lambda x: (x.sort(), x)[1])(list(str(phi)))) and w / phi < val:
            val = w / phi
            ans = w

print(ans)

```
