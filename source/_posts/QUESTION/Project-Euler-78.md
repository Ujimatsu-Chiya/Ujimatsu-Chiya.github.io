---
title: Project Euler 78
category:
  - Project Euler
tags:
  - OEIS
mathjax: true
date: 2022-05-02 16:36:41
---

<escape><!-- more --></escape>

# Project Euler 78

## 题目

### Coin partitions

Let $p(n)$ represent the number of different ways in which $n$ coins can be separated into piles. For example, five coins can separated into piles in exactly seven different ways, so $p(5)=7$.

OOOOO<br>
OOOO O<br>
OOO OO<br>
OOO O O<br>
OO OO O<br>
OO O O O<br>
O O O O O

Find the least value of $n$ for which $p(n)$ is divisible by one million.

## 解决方案

本题所使用的的状态转移方程和第76题完全一致。不过，由于本体求的是第一个$p(n)$能被$10^6$整除，因此需要更快的方法。

将$p(n)$的前一些项放进OEIS查询，结果为[A000041](https://oeis.org/A000041)。

在Formula一栏中可以发现以下信息：

```
a(n) - a(n-1) - a(n-2) + a(n-5) + a(n-7) - a(n-12) - a(n-15) + ... = 0, where the sum is over n-k and k is a generalized pentagonal number (A001318) <= n and the sign of the k-th term is (-1)^([(k+1)/2]). See A001318 for a good way to remember this!
```

其中，数列[A001318](https://oeis.org/A001318)是一种广义五边形数。

另外，符号位由确定广义五边形数的自变量的绝对值决定。

处理以上各种细节，最终可以得到$p(n)$的式子为：

$$
p(n)=
\left \{\begin{aligned}
  &1  & & \mathrm{if\quad} n=0  \\
  &\sum_{m}^{|m|\ge1,\frac{m(3m-1)}{2}\leq n}(-1)^{m+1}p(n-\frac{m(3m-1)}{2}) & & \mathrm{else}
\end{aligned}\right.
$$

由于广义五边形数增长是二次的，因此计算$p(N)$的时间复杂度缩减到了$O(N\sqrt{N})$。

## 代码

```py
from itertools import count

mod = 10 ** 6


def gen_pentagonal():
    for i in count(1, 1):
        yield i * (3 * i - 1) // 2
        yield i * (3 * i + 1) // 2


p = [1]

for n in count(1, 1):
    i = 0
    val = 0
    for m in gen_pentagonal():
        if m > n:
            break
        sgn = i >> 1 & 1
        if sgn == 0:
            val = (val + p[n - m]) % mod
        else:
            val = (val - p[n - m] + mod) % mod
        i += 1
    if val == 0:
        ans = n
        break
    p.append(val)
print(ans)

```
