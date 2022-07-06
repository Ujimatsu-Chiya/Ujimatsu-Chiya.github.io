---
title: Project Euler 293
tags:
  - Project Euler
mathjax: true
date: 2022-07-06 13:08:05
---

<escape><!-- more --></escape>

# Project Euler 293

## 题目

### Pseudo-Fortunate Numbers

An even positive integer $N$ will be called admissible, if it is a power of $2$ or its distinct prime factors are consecutive primes.

The first twelve admissible numbers are $2,4,6,8,12,16,18,24,30,32,36,48$.

If $N$ is admissible, the smallest integer $M > 1$ such that $N+M$ is prime, will be called the pseudo-Fortunate number for $N$.

For example, $N=630$ is admissible since it is even and its distinct prime factors are the consecutive primes $2,3,5$ and $7$.

The next prime number after $631$ is $641$; hence, the pseudo-Fortunate number for $630$ is $M=11$.

It can also be seen that the pseudo-Fortunate number for $16$ is $3$.

Find the sum of all distinct pseudo-Fortunate numbers for admissible numbers $N$ less than $10^9$.

## 解决方案

由于可接受数$N$是一个偶数，并且质因子是连续的。那么$N$就是形如这种形式：$2^a,2^a\cdot 3^b,2^a\cdot3^b\cdot5^c,\dots$。总之，一个质因子被使用了，那么它前面的质因子也要被使用。

那么这些数其实数量很少，并且最大质因子其实也很小，因此考虑直接枚举$N$。

每枚举一个$N$，那么求对应的$M$，相当于求大于$N+1$的下一个质数。一个数的下一个质数通过素性测试算法直接枚举就不难找到。本代码直接使用sympy库的nextprime方法。

## 代码

```py
from sympy import nextprime

N = 10 ** 9
pr = []
M = p = 1
while True:
    p = nextprime(p)
    M *= p
    if M >= N:
        break
    pr.append(p)
st = set()


def dfs(f: int, n: int):
    if f == len(pr):
        return
    while True:
        n *= pr[f]
        if n >= N:
            break
        st.add(nextprime(n + 1) - n)
        dfs(f + 1, n)


dfs(0, 1)
ans = sum(st)
print(ans)

```
