---
title: Project Euler 263
category:
  - Project Euler
tags:
mathjax: true
date: 2022-08-05 21:40:32
---

<escape><!-- more --></escape>

# Project Euler 263

## 题目

### An engineers’ dream come true

Consider the number $6$. The divisors of $6$ are: $1,2,3$ and $6$.

Every number from $1$ up to and including $6$ can be written as a sum of distinct divisors of $6$:

$1=1, 2=2, 3=1+2, 4=1+3, 5=2+3, 6=6.$

A number $n$ is called a practical number if every number from $1$ up to and including $n$ can be expressed as a sum of distinct divisors of $n$.

A pair of consecutive prime numbers with a difference of six is called a sexy pair (since “sex” is the Latin word for “six”). The first sexy pair is $(23, 29)$.

We may occasionally find a triple-pair, which means three consecutive sexy prime pairs, such that the second member of each pair is the first member of the next pair.

We shall call a number $n$ such that:

- $(n-9, n-3), (n-3,n+3), (n+3, n+9)$ form a triple-pair, and
- the numbers $n-8, n-4, n, n+4$ and $n+8$ are all practical,

an engineers’ paradise.

Find the sum of the first four engineers’ paradises.

## 解决方案

这个[页面](https://en.wikipedia.org/wiki/Practical_number)给出了实际数的一个高效的判定：

令$n$的分解为$\prod_{i=1}^k p_i^{e_i}$，并且有$p_1<p_2<\dots,p_k$。$n$是实际数当且仅当对于所有$1<i\le k$，都满足：

$$p_i\le 1+\sigma(\prod_{j=1}^{i-1} p_j^{e_j})=1+\prod_{j=1}^{i-1} \dfrac{p_j^{e_j+1}-1}{p_j-1}$$

其中$\sigma(n)$是$n$的所有因数之和。

并且，这个页面还提出了，除了$1,2$，所有实际数必定是$4$或者是$6$的倍数。

接下来单独考虑每个数$2\sim 8$和候选数$n$的各种可能情况：

### $2$

$n-3$是质数，因此$2\mid n$。

### $3$

$n-3$是质数，因此$3\nmid n$。

### $4$

根据$2$的情况，要么$n=4k_4$，要么$n=4k_4+2$.

当$n=4_k+2$时，$n-8,n-4,n,n+4,n+8$都不是$4$的倍数，但是无论$k$取什么，总有一个数不是$3$的倍数。因此$4\mid n$。

### $5$

由于$n-9,n-3,n+3,n+9$都是质数，只有当$n\equiv 0 \pmod 5$时，这$4$个数都不是$5$的倍数。

### $7$

由于$n-9,n-3,n+3,n+9$都是质数，因此$n\equiv 0\text{ or }1\text{ or } 6 \pmod 7$。

### $8$

仅讨论$n=8k_8,8k_8+4$时的情况。为了使得$n+8,n-8$是实用数，那么它们的**次小**质因子中，其中一个必须为$3$，另一个必须为$7$（不是$5$的原因是$5\mid n$），这种情况下只有当$n=8k_8+4$时才满足。

在这种情况下，同样只有当$n\equiv 1\pmod 7$时满足。

综上所述，通过中国剩余定理，联立以下式子：

$$\begin{aligned}
&n\equiv 1, 2\pmod 3\\
&n\equiv 0\pmod 5\\
&n\equiv 1\pmod 7\\
&n\equiv 4\pmod 8
\end{aligned}$$

得到当$n\equiv \pm 20\pmod {840}$时，$n$才有可能是一个答案。

暴力求出所有候选值，并进行判断即可。

## 代码

```PY
from itertools import count
from sympy import nextprime
from tools import factorization, is_prime

Q = 4


def is_practical(n):
    mul = 1
    for p, e in factorization(n):
        if p > 1 + mul:
            return False
        mul *= (p ** (e + 1) - 1) // (p - 1)
    return True


def gen():
    for n in count(0, 840):
        yield n + 20
        yield n + 820


ans = 0
for x in gen():
    if is_prime(x - 9) and is_prime(x - 3) and is_prime(x + 3) and is_prime(x + 9):
        if is_practical(x - 8) and is_practical(x - 4) and is_practical(x) and is_practical(x + 4) and is_practical(
                x + 8):
            if nextprime(x - 9) == x - 3 and nextprime(x - 3) == x + 3 and nextprime(x + 3) == x + 9:
                ans += x
                Q -= 1
                if Q == 0:
                    break

print(ans)

```
