---
title: Project Euler 50
category:
  - Project Euler
tags:
mathjax: true
date: 2022-04-27 23:32:58
---

<escape><!-- more --></escape>

# Project Euler 50

## 题目

### Consecutive prime sum

The prime $41$, can be written as the sum of six consecutive primes:

$$41 = 2 + 3 + 5 + 7 + 11 + 13$$

This is the longest sum of consecutive primes that adds to a prime below one-hundred.

The longest sum of consecutive primes below one-thousand that adds to a prime, contains $21$ terms, and is equal to $953$.

Which prime, below one-million, can be written as the sum of the most consecutive primes?

## 解决方案

可以先将小于$N=10^6$的质数筛选出来，然后做一遍前缀和。

接下来，找到最大的前缀长度$l$，使得前$l$个质数和小于$N$。

从前缀长度$l$往下遍历，在遍历这个前缀长度$i$时，看看有没有一个长度为$i$的子数组其和是一个质数。如果找到了，这就是一个全局最优解并退出。
如果找不到，那么就需要判断子数组和是否超过$N$，超过了就及时退出循环，继续寻找$i-1$时的解。

## 代码

```py
from tools import get_prime

N = 1000000
pr = get_prime(N)
st = set(pr)
s = [0]
for x in pr:
    s.append(s[-1] + x)
for i in range(len(pr)):
    if s[i] > N:
        p = i
        break
for l in range(p, 0, -1):
    ok = False
    for i in range(l, len(pr) + 1):
        if s[i] - s[i - l] in st:
            ans = s[i] - s[i - l]
            ok = True
            break
        if s[i] - s[i - l] > N:
            break
    if ok:
        break
print(ans)

```
