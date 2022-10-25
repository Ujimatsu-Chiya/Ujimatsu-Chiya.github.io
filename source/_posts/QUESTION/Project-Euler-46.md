---
title: Project Euler 46
category:
  - Project Euler
tags:
mathjax: true
date: 2022-04-30 10:31:16
---

<escape><!-- more --></escape>

# Project Euler 46

## 题目

### Goldbach’s other conjecture

It was proposed by Christian Goldbach that every odd composite number can be written as the sum of a prime and twice a square

$\begin{aligned}
9 &= 7 + 2×1^2 \\
15 &= 7 + 2×2^2 \\
21 &= 3 + 2×3^2 \\
25 &= 7 + 2×3^2 \\
27 &= 19 + 2×2^2 \\
33 &= 31 + 2×1^2\\
\end{aligned}$

It turns out that the conjecture was false.
What is the smallest odd composite that cannot be written as the sum of a prime and twice a square?

## 解决方案

从小到大先遍历每个奇数$n$，如果是合数，那就直接枚举$2i^2$，再判断$n-2i^2$是否为质数。否则就把当前素数添加进集合。

可以发现这个数比较小，因此这种做法速度比较快。

## 代码

```py
from itertools import count
from tools import is_prime

pr = {2}
for n in count(3, 2):
    if is_prime(n):
        pr.add(n)
    else:
        ok = False
        for i in count(1, 1):
            res = n - 2 * i * i
            if res <= 0:
                break
            if res in pr:
                ok = True
                break
        if not ok:
            ans = n
            break
print(ans)
```
