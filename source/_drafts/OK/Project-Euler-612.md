---
title: Project Euler 612
tags:
  - Project Euler
mathjax: true
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