---
title: Project Euler 119
tags:
  - Project Euler
mathjax: true
date: 2022-05-06 22:24:29
---

<escape><!-- more --></escape>

# Project Euler 119

## 题目

### Digit power sum

The number $512$ is interesting because it is equal to the sum of its digits raised to some power: $5 + 1 + 2 = 8$, and $8^3 = 512$. Another example of a number with this property is $614656 = 28^4$.

We shall define $a_n$ to be the $n^\mathrm{th}$ term of this sequence and insist that a number must contain at least two digits to have a sum.

You are given that $a_2 = 512$ and $a_{10} = 614656$.

Find $a_{30}$.

## 解决方案

本题所需要求的数，必定是形如$a^b(a,b>1)$的数。因此，先枚举$a$到足够大（本代码设定为$5N$）时，再枚举$b$，之后计算$a^b$的数位和。当数位和远远大于$a$时（因为这里有$0$的存在，在计算$a^b$的数位和时，有可能虽然数$a^b$很大，但是因为$0$很多数位和很小），才停止循环。

最终排序，导出结果即可。

## 代码

```py
from itertools import count

N = 30
ls = []

for a in range(2, N * 5 + 1):
    for b in count(2, 1):
        y = sum(int(w) for w in str(a ** b))
        if y == 1 or y > 10 * a:
            break
        if y == a:
            ls.append(a ** b)
ls.sort()
ans = ls[N - 1]
print(ans)


```
