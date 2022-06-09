---
title: Project Euler 133
tags:
  - Project Euler
mathjax: true
date: 2022-05-06 22:22:55
---

<escape><!-- more --></escape>

# Project Euler 133

## 题目

### Repunit nonfactors

A number consisting entirely of ones is called a repunit. We shall define $R(k)$ to be a repunit of length $k$; for example, $R(6) = 111111$.

Let us consider repunits of the form $R(10^n)$.

Although $R(10)$, $R(100)$, or $R(1000)$ are not divisible by $17$, $R(10000)$ is divisible by $17$. Yet there is no value of $n$ for which $R(10^n)$ will divide by $19$. In fact, it is remarkable that $11, 17, 41$, and $73$ are the only four primes below one-hundred that can  be a factor of $R(10^n)$.

Find the sum of all the primes below one-hundred thousand that will never be a factor of $R(10^n)$.

## 乘法群

设$\mathbb{Z}_{m}^*$为模数为$m$的乘法群。容易知道，乘法群是个循环群，而且其大小为$\varphi(m)$，其中$\varphi$为欧拉函数。

元素$a$在群$\mathbb{Z}_{m}^*$上的阶$\lambda_m(a)$：使得$a^k \equiv 1(\mod m)$的最小正整数$k$。

需要注意，一个元素的阶是群的大小的因数，也就是有$\forall a \in \mathbb{Z}_m^*,\lambda_m(a)|\varphi(m)$。

## 解决方案

对于所有非$2$和$5$的质数$p$，容易知道$\gcd(10,9p)=1$，因此$10\in \mathbb{Z}_{9m}^*$。

因此，如果一个质因数$p$永远不可能为$R(10^n)$的阶，也就是永远不会存在$n$满足以下等式：

$$10^{10^n}\equiv 1(\mod 9p)$$

那么，就说明不存在$n$，使得$\lambda_{9p}(10)|10^n$。

因此，找出$\varphi(9p)$的所有因数，然后从小到大判断这个因数是不是$10$在群$\mathbb{Z}_{9m}^*$中的阶，最终计算出$\lambda_{9p}(10)$。

由于$10^n$只有质因数$2,5$。因此，如果$\lambda_{9p}(10)|10^n$，那么$\lambda_{9p}(10)$就必须只有质因数$2,5$。

本代码使用sympy库中的n_order(a,m)函数计算$\lambda_m(a)$的值。

## 代码

```py
from tools import get_prime, divisors

N = 10 ** 5
pr = get_prime(N)
ans = 0
N = 100000
for x in pr:
    if x <= 5:
        ans += x
        continue
    # phi(9x) = 6(x-1)
    phi = 6 * (x - 1)
    ls = divisors(phi)
    for k in ls:
        if pow(10, k, 9 * x) == 1:
            order = k
            break
    while order % 5 == 0:
        order //= 5
    while order & 1 == 0:
        order >>= 1
    if order != 1:
        ans += x
print(ans)

```

```py
from sympy import n_order
from tools import get_prime

N = 10 ** 5
pr = get_prime(N)
ans = 0
N = 100000
for x in pr:
    if x <= 5:
        ans += x
        continue
    order = n_order(10, 9 * x)
    while order % 5 == 0:
        order //= 5
    while order & 1 == 0:
        order >>= 1
    if order != 1:
        ans += x
print(ans)

```
