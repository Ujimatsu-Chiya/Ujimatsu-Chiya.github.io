---
title: Project Euler 506
category:
  - Project Euler
tags:
mathjax: true
date: 2022-07-13 22:57:43
---

<escape><!-- more --></escape>

# Project Euler 506

## 题目

### Clock sequence

Consider the infinite repeating sequence of digits:

$$1234321234321234321\dots$$

Amazingly, you can break this sequence of digits into a sequence of integers such that the sum of the digits in the $n$’th value is $n$.

The sequence goes as follows:

$$1, 2, 3, 4, 32, 123, 43, 2123, 432, 1234, 32123, \dots$$

Let $v_n$ be the $n$’th value in this sequence. For example, $v_2=2, v_5=32$ and $v_{11}=32123$.

Let $S(n)$ be $v_1+v_2+\dots+v_n$. For example, $S(11)=36120$, and $S(1000) \bmod 123454321 = 18232686$.

Find $S(10^{14})\bmod 123454321$.

## 解决方案

打印数列的前$40$项，发现如下规律：

```
1
2
3
4
32
123
43
2123
432
1234
32123
43212
34321
23432
123432
1       234321
2       343212
3       432123
4       321234
32      123432
123     432123
43      212343
2123    432123
432     123432
1234    321234
32123   432123
43212   343212
34321   234321
23432   123432
123432  123432
1       234321      234321
2       343212      343212
3       432123      432123
4       321234      321234
32      123432      123432
123     432123      432123
43      212343      212343
2123    432123      432123
432     123432      123432
1234    321234      321234
```

单独拿出第$2,17,32$项，可以看出：

```
2
2       343212
2       343212      343212
```

第$i$个数是第$i-15$个数后面拼接一个固定的$6$位数，因此分开考虑，使用等比数列的前缀和进行计算即可。注意计算循环添加的那一部分数，相当于是等比数列**前缀和的前缀和**。

## 代码

```py
from tools import mod_inverse

N = 10 ** 14
mod = 123454321
inv = mod_inverse(10 ** 6 - 1, mod)
m = 10 ** 6
a = [1, 2, 3, 4, 32, 123, 43, 2123, 432, 1234, 32123, 43212, 34321, 23432, 123432]
b = [234321, 343212, 432123, 321234, 123432, 432123, 212343, 432123, 123432, 321234, 432123, 343212, 234321, 123432,
     123432]
T = len(a)
ans = 0
for i in range(T):
    cnt = N // T + (i < N % T)
    c1 = (pow(m, cnt, mod) - 1) * inv % mod
    c2 = (c1 - cnt) * inv % mod
    ans = (ans + a[i] * c1 + b[i] * c2) % mod
print(ans)

```
