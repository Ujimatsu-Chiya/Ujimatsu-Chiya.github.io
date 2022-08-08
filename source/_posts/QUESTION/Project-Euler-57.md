---
title: Project Euler 57
category:
  - Project Euler
tags:
mathjax: true
date: 2022-04-30 10:31:47
---

<escape><!-- more --></escape>

# Project Euler 57

## 题目

### Square root convergents

It is possible to show that the square root of two can be expressed as an infinite continued fraction.
$$\sqrt 2 =1+ \dfrac 1 {2+ \dfrac 1 {2 +\dfrac 1 {2+ \dots}}}$$
By expanding this for the first four iterations, we get:

$1 + \dfrac 1 2 = \dfrac  32 = 1.5$

$1 + \dfrac 1 {2 + \dfrac 1 2} = \dfrac 7 5 = 1.4$

$1 + \dfrac 1 {2 + \dfrac 1 {2+\dfrac 1 2}} = \dfrac {17}{12} = 1.41666 \dots$

$1 + \dfrac 1 {2 + \dfrac 1 {2+\dfrac 1 {2+\dfrac 1 2}}} = \dfrac {41}{29} = 1.41379 \dots$

The next three expansions are $\dfrac {99}{70}$, $\dfrac {239}{169}$, and $\dfrac {577}{408}$, but the eighth expansion, $\dfrac {1393}{985}$, is the first example where the number of digits in the numerator exceeds the number of digits in the denominator.

In the first one-thousand expansions, how many fractions contain a numerator with more digits than the denominator?

## 解决方案

观察上面的连分数，将其写成一个序列$a_1,a_2,a_3,\dots$，容易发现规律：
$$a_n=\frac{1}{1+a_{n-1}}+1$$
因此，直接通过此式子进行$1000$次迭代求出每个序列的值。

本代码使用的是fractions库中的Fraction类，它用于维护一个分数的类型。

## 代码

```py
from fractions import Fraction

N = 1000
a = Fraction(1, 1)
ans = 0
for i in range(1000):
    a = 1 / (1 + a) + 1
    if len(str(a.numerator)) > len(str(a.denominator)):
        ans += 1
print(ans)

```
