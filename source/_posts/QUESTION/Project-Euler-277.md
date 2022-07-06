---
title: Project Euler 277
tags:
  - Project Euler
mathjax: true
date: 2022-07-06 13:08:54
---

<escape><!-- more --></escape>

# Project Euler 277

## 题目

### A Modified Collatz sequence

A modified Collatz sequence of integers is obtained from a starting value $a_1$ in the following way:

$a_{n+1} = \dfrac {a_n} 3\quad$ if $a_n$ is divisible by $3$. We shall denote this as a large downward step, "D".

$a_{n+1} = \dfrac {4 a_n+2} 3\quad$ if $a_n$ divided by $3$ gives a remainder of $1$. We shall denote this as an upward step, "U".

$a_{n+1} = \dfrac {2 a_n -1} 3\quad$ if $a_n$ divided by $3$ gives a remainder of $2$. We shall denote this as a small downward step, "d".

The sequence terminates when some $a_n = 1$.

Given any integer, we can list out the sequence of steps.

For instance if $a_1=231$, then the sequence $\{a_n\}=\{231,77,51,17,11,7,10,14,9,3,1\}$ corresponds to the steps "DdDddUUdDD".

Of course, there are other sequences that begin with that same sequence "DdDddUUdDD...".

For instance, if $a_1=1004064$, then the sequence is DdDddUUdDDDdUDUUUdDdUUDDDUdDD.

In fact, $1004064$ is the smallest possible $a_1 > 10^6$ that begins with the sequence DdDddUUdDD.

What is the smallest $a_1 > 10^{15}$ that begins with the sequence "UDDDUdddDDUDDddDdDddDDUDDdUUDd"?

## 解决方案

令$N=10^{15}$,s="UDDDUdddDDUDDddDdDddDDUDDdUUDd"，并且字符串$s$的长度为$M$.

并且注意到，上面三个递推式都是线性变换。

如果一开始$a_1$是一个已知的数$x$，那么经过这么多的递推变换后，最终得到的值是一个形如$kx+b$的数。注意$k,b$都是分数，但是$kx+b$是一个正整数，设这个正整数为$y$.

不难发现$k,b$的分母是$3^M$，那么将$k$和$b$分别写成$\dfrac{u}{3^M},\dfrac{v}{3^M}$，那么可以得到一个等式：

$$ux-3^My=-v$$

最终，我们可以使用扩展欧几里得算法解上面的方程，得出一个$x$，并且这个$x$将比$N$大。这个$x$最终是本题的答案。

## 代码

```py
from fractions import Fraction

N = 10 ** 15
S = "UDDDUdddDDUDDddDdDddDDUDDdUUDd"


def ex_gcd(a: int, b: int):
    if b == 0:
        return 1, 0, a
    else:
        x, y, g = ex_gcd(b, a % b)
        return y, x - (a // b) * y, g


k = Fraction(1)
b = Fraction(0)
for ch in S:
    if ch == 'U':
        k = k * 4 / 3
        b = (b * 4 + 2) / 3
    elif ch == 'D':
        k /= 3
        b /= 3
    else:
        k = k * 2 / 3
        b = (b * 2 - 1) / 3
u, n, v = k.numerator, k.denominator, b.numerator
x, _, _ = ex_gcd(u, n)
x = x * -v % n
d = (N - x + n - 1) // n
ans = x + d * n
print(ans)

```
