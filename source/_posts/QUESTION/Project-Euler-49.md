---
title: Project Euler 49
category:
  - Project Euler
tags:
mathjax: true
date: 2022-04-30 10:31:24
---

<escape><!-- more --></escape>


# Project Euler 49
## 题目
### Prime permutations
The arithmetic sequence, $1487, 4817, 8147$, in which each of the terms increases by $3330$, is unusual in two ways: (i) each of the three terms are prime, and, (ii) each of the 4-digit numbers are permutations of one another.

There are no arithmetic sequences made up of three $1$-, $2$-, or $3$-digit primes, exhibiting this property, but there is one other $4$-digit increasing sequence.

What $12$-digit number do you form by concatenating the three terms in this sequence?

## 解决方案

预处理出所有$4$位质数，并将使用相同数位的质数存放在一起。

处于同一集合下的所有同数位的质数，最多只有$4!=24$个。因此可以直接暴力枚举，看看是否存在三个数为等差数列。


## 代码

```py
from tools import get_prime

M = 4
pr = get_prime(10 ** M - 1)
mp = {}
for p in pr:
    if p >= 10 ** (M - 1):
        s = "".join((lambda x: (x.sort(), x)[1])(list(str(p))))
        if s not in mp.keys():
            mp[s] = []
        mp[s].append(p)

ls = []
for v in mp.values():
    for i in range(len(v)):
        for j in range(i + 1, len(v)):
            for k in range(j + 1, len(v)):
                if v[j] + v[j] == v[i] + v[k]:
                    ls.append(str(v[i]) + str(v[j]) + str(v[k]))

ans = ls[1]
print(ans)

```