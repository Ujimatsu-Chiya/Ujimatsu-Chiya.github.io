---
title: Project Euler 225
tags:
  - Project Euler
mathjax: true
date: 2022-06-05 09:28:36
---

<escape><!-- more --></escape>

# Project Euler 225

## 题目

### Tribonacci non-divisors

The sequence $1, 1, 1, 3, 5, 9, 17, 31, 57, 105, 193, 355, 653, 1201 \dots$ is defined by $T_1 = T_2 = T_3 = 1$ and $T_n = T_n-1 + T_n-2 + T_n-3$.

It can be shown that $27$ does not divide any terms of this sequence.

In fact, $27$ is the first odd number with this property.

Find the $124^{\text{th}}$ odd number that does not divide any terms of the above sequence.

## 解决方案

模$p$下的广义斐波那契序列必定是一个周期性序列。因为它的下一个数都是由最近的$m$个数（这里为$m=3$）相加决定的，这些数最多只有$p^m$种不同的可能性。也就是说，决定下一个数是多少的状态是有限的。最终无限的序列必定会呈现一个周期性。

因此，利用这种性质，可以寻找序列的模$p$周期，从而判断出这个奇数是否不能将原序列中任何一个数相除。

## 代码

```py
from itertools import count

Q = 124
cnt = 0
for m in count(27, 2):
    ok = 1
    a = b = c = 1
    while True:
        a, b, c = b, c, (a + b + c) % m
        if c == 0:
            ok = 0
            break
        if a == b == c == 1:
            break
    if ok:
        cnt += 1
        if cnt == Q:
            ans = m
            break
print(ans)

```
