---
title: Project Euler 234
category:
  - Project Euler
tags:
mathjax: true
date: 2022-06-08 22:37:29
---

<escape><!-- more --></escape>

# Project Euler 234

## 题目

### Semidivisible numbers

For an integer $n \ge 4$, we define the *lower prime square root* of n, denoted by $\text{lps}(n)$, as the largest prime $\le \sqrt{n}$ and the *upper prime square root* of $n$, $\text{ups}(n)$, as the smallest prime $\ge \sqrt{n}$.

So, for example, $\text{lps}(4) = 2 = \text{ups}(4), \text{lps}(1000) = 31, \text{ups}(1000) = 37$.

Let us call an integer $n \ge 4$ *semidivisible*, if one of $\text{lps}(n)$ and $\text{ups}(n)$ divides $n$, but not both.

The sum of the semidivisible numbers not exceeding $15$ is $30$, the numbers are $8, 10$ and $12$. $15$ is not semidivisible because it is a multiple of both $\text{lps}(15)=3$ and $\text{ups}(15)=5$.

As a further example, the sum of the $92$ semidivisible numbers up to $1000$ is $34825$.

What is the sum of all semidivisible numbers not exceeding $999966663333$ ?

## 解决方案

当一个数$n$是一个质数$p$的平方数时，$\text{lps}(n) = \text{ups}(n)$。这种数不属于本题考虑的范围内；

否则，$\text{lps}(n),\text{ups}(n)$是两个相邻的质数（因为它们以$\sqrt{n}$为分界点）。

令$p$为一个质数，$q$是和$p$相邻并且大于$p$质数。那么$\forall p^2<x<q^2,\text{lps}(x)=p,\text{ups}(x)=q$。

每次枚举到一对相邻的质数$(p,q)$，我们可以在**开区间**$(p^2,q^2)$寻找所有只被$p,q$之一整除的数。尽管区间$(p^2,q^2)$范围很大，但是枚举步长是$p$，因此其实每个区间中枚举的数量是很少的。

也可以通过容斥原理加速计算，省去枚举的时间。

## 代码

```py
from tools import get_prime

N = 999966663333
pr = get_prime(int(N ** 0.5 + 4))
ans = 0
for i in range(1, len(pr)):
    vl, vr = pr[i - 1], pr[i]
    for v in range((vl * vl + vr - 1) // vr * vr, min(N + 1, vr * vr), vr):
        if v % vl:
            ans += v
    for v in range(vl * (vl + 1), min(N + 1, vr * vr), vl):
        if v % vr:
            ans += v
print(ans)

```

```py
from tools import get_prime

N = 999966663333


def cal(l, r, v):
    l, r = (l - 1) // v, r // v
    return (r * (r + 1) // 2 - l * (l + 1) // 2) * v


pr = get_prime(int(N ** 0.5 + 4))
ans = 0
for i in range(1, len(pr)):
    vl, vr = pr[i - 1], pr[i]
    l, r = min(vl * vl + 1, N + 1), min(vr * vr - 1, N + 1)
    # pq的倍数被算了两次，所以要减去两次。
    ans += cal(l, r, vl) + cal(l, r, vr) - cal(l, r, vl * vr) * 2
print(ans)

```
