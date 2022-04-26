---
title: Project Euler 21
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>

# Project Euler 21
## 题目
### Amicable numbers
Let $d(n)$ be defined as the sum of proper divisors of $n$ (numbers less than $n$ which divide evenly into $n$). 

If $d(a) = b$ and $d(b) = a$, where $a \neq b$, then $a$ and $b$ are an amicable pair and each of $a$ and $b$ are called amicable numbers.

For example, the proper divisors of $220$ are $1$, $2$, $4$, $5$, $10$, $11$, $20$, $22$, $44$, $55$ and $110$; therefore $d(220) = 284$. The proper divisors of $284$ are $1$, $2$, $4$, $71$ and $142$; so $d(284) = 220$.
Evaluate the sum of all the amicable numbers under $10000$.
## 因数和定理
如果一个正整数$n$分解后成为：
$$n=\prod p_i^{e_i}$$
那么$n$的因数的和为：
$$\prod \dfrac{p_i^{e_i+1}-1}{p_i-1}$$

## 解决方案
可以直接通过因数和定理，先将所有$10000$以下的数进行分解，然后计算出真因数的值。
最后直接判断两对数是否满足亲和数的条件。

计算$1\sim n$中的所有因数和也可以通过欧拉筛加速计算。

## 代码
```py
from tools import factorization

N = 10000
d = [0 for _ in range(N)]
for i in range(1, N):
    ls = factorization(i)
    w = 1
    for p, e in ls:
        w *= (p ** (e + 1) - 1) // (p - 1)
    d[i] = w - i
ans = 0
for i in range(1, N):
    if N > d[i] > i == d[d[i]]:
        ans += i + d[i]
print(ans)
```
