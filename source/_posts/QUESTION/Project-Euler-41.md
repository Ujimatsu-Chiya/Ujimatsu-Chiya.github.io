---
title: Project Euler 41
category:
  - Project Euler
tags:
mathjax: true
date: 2022-04-27 23:32:37
---

<escape><!-- more --></escape>

# Project Euler 41

## 题目

### Pandigital prime

We shall say that an $n$-digit number is pandigital if it makes use of all the digits $1$ to $n$ exactly once. For example, $2143$ is a $4$-digit pandigital and is also prime.

What is the largest $n$-digit pandigital prime that exists?

## 解决方案

观察前$9$项$1\sim n$中所有数之和$p(n)=\dfrac{n(n+1)}{2}$的值：

$$1,3,6,10,15,21,28,36,45$$

可以发现，当$n\neq 1,4,7$时，$p(n)\equiv 0 \pmod 3$。

这说明在其它情况下，无论里面的数位排列如何，它们都是$3$的倍数，故对这一部分的数不需要进行判断。

对于剩下的数，用`itertools`库中的`permutations`对每一个排列进行遍历，并判断拼成的数是不是质数。

判断大质数使用`gmpy2`中的`is_prime`，它会以$2^{-64}$的概率将一个合数判断成质数。这个函数将会封装在自定义的`tools`工具包中。

## 代码

```py
from itertools import permutations
from gmpy2 import is_prime

ls = [7, 4, 1]
ok = False
for n in ls:
    per = permutations([n - i for i in range(n)])
    for p in per:
        w = int("".join(str(x) for x in p))
        if is_prime(w):
            ans = w
            ok = True
            break
    if ok:
        break
print(ans)

```
