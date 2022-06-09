---
title: Project Euler 65
tags:
  - Project Euler
mathjax: true
date: 2022-04-30 10:32:16
---

<escape><!-- more --></escape>

# Project Euler 65

## 题目

### Convergents of e

The square root of $2$ can be written as an infinite continued fraction.

$\sqrt{2} = 1 + \dfrac{1}{2 + \dfrac{1}{2 + \dfrac{1}{2 + \dfrac{1}{2 + \dots}}}}$

The infinite continued fraction can be written, $\sqrt{2} = [1; (2)]$, $(2)$ indicates that 2 repeats *ad infinitum*. In a similar way, $\sqrt{23} = [4; (1, 3, 1, 8)]$.

It turns out that the sequence of partial values of continued fractions for square roots provide the best rational approximations. Let us consider the convergents for $\sqrt{2}$.

$1 + \dfrac{1}{2} = \dfrac{3}{2} $
$1 + \dfrac{1}{2 + \dfrac{1}{2}} = \dfrac{7}{5}$
$1 + \dfrac{1}{2 + \dfrac{1}{2 + \dfrac{1}{2}}} = \dfrac{17}{12}$
$1 + \dfrac{1}{2 + \dfrac{1}{2 + \dfrac{1}{2 + \dfrac{1}{2}}}} = \dfrac{41}{29}$

Hence the sequence of the first ten convergents for $\sqrt{2}$ are:

$1, \dfrac{3}{2}, \dfrac{7}{5}, \dfrac{17}{12}, \dfrac{41}{29}, \dfrac{99}{70}, \dfrac{239}{169}, \dfrac{577}{408}, \dfrac{1393}{985}, \dfrac{3363}{2378}, ...$

What is most surprising is that the important mathematical constant,$e = [2; 1, 2, 1, 1, 4, 1, 1, 6, 1, \dots , 1, 2k, 1, \dots]$.

The first ten terms in the sequence of convergents for $e$ are:

$2, 3, \dfrac{8}{3}, \dfrac{11}{4}, \dfrac{19}{7}, \dfrac{87}{32}, \dfrac{106}{39}, \dfrac{193}{71}, \dfrac{1264}{465}, \dfrac{1457}{536}, ...$

The sum of digits in the numerator of the $10^{\mathrm{th}}$ convergent is $1 + 4 + 5 + 7 = 17$.

Find the sum of digits in the numerator of the $100 ^{\mathrm{th}}$ convergent of the continued fraction for $e$.

## 解决方案

假设连分数序列为$a$，那么根据连分数的产生规则，第$n$个逼近值$b_{n,1}$如下构造：

$$b_{n,i}=
\left \{\begin{aligned}
  &a_n  & & \mathrm{if\quad} i=n \\
  &a_i+\dfrac{1}{b_{n,i+1}} & & \mathrm{else}
\end{aligned}\right.
$$

直接使用分数进行模拟即可。

## 代码

```py
from fractions import Fraction

N = 100
a = [2]
v = 0
for i in range(1, N + 1):
    a += [1, 2 * i, 1]
t = a[:N][::-1]
w = Fraction(t[0])
for i in range(1, len(t)):
    w = 1 / w + t[i]
ans = sum(int(x) for x in str(w.numerator))
print(ans)

```
