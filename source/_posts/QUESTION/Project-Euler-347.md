---
title: Project Euler 347
category:
  - Project Euler
tags:
mathjax: true
date: 2022-06-22 23:27:28
---

<escape><!-- more --></escape>

# Project Euler 347

## 题目

### Largest integer divisible by two primes

The largest integer $\le 100$ that is only divisible by both the primes $2$ and $3$ is $96$, as $96=32*3=2^5*3$.

For two *distinct* primes $p$ and $q$ let $M(p,q,N)$ be the largest positive integer $\le N$ only divisible by both $p$ and $q$ and $M(p,q,N)=0$ if such a positive integer does not exist.

E.g. $M(2,3,100)=96$.

$M(3,5,100)=75$ and not $90$ because $90$ is divisible by $2 ,3$ and $5$.

Also $M(2,73,100)=0$ because there does not exist a positive integer $\le 100$ that is divisible by both $2$ and $73$.

Let $S(N)$ be the sum of all distinct $M(p,q,N)$.
$S(100)=2262.$

Find $S(10 000 000)$.

## 解决方案

根据分解质因数的思想可以知道，如果$p,q$有其中一个不相同，那么$M(p,q,N)$也不会相同。

因此，令$N=10000000$，枚举所有的$p,q(p< q)$使得$pq\le N$。那么找到一对$(x,y)$使得$p^xq^y\le N$并且$p^xq^y$最大，那么$p^xq^y$便是其中一个答案。

另外一个地方则是，质数只需要筛选到$\dfrac{N}{2}$即可。因为枚举的$(p,q)$中，$p$至少为$2$，那么$q$最多为$\dfrac{N}{2}$。

## 代码

```py
from tools import get_prime

N = 10 ** 7
pr = get_prime(N // 2)
ans = 0
for i in range(len(pr) - 1):
    for j in range(i + 1, len(pr)):
        if pr[i] * pr[j] > N:
            break
        mx = 0
        x = pr[i]
        while x * pr[j] <= N:
            y = pr[j]
            while x * y <= N:
                mx = max(mx, x * y)
                y *= pr[j]
            x *= pr[i]
        ans += mx
print(ans)

```
