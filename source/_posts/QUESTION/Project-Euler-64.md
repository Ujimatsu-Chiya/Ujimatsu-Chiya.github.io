---
title: Project Euler 64
category:
  - Project Euler
tags:
  - 论文
mathjax: true
date: 2022-05-03 09:22:17
---

<escape><!-- more --></escape>

# Project Euler 64

## 题目

### Odd period square roots

All square roots are periodic when written as continued fractions and can be written in the form:

$\sqrt{N}=a_0+\dfrac 1 {a_1+\dfrac 1 {a_2+ \dfrac 1 {a_3+ \dots}}}$

For example, let us consider $\sqrt{23}:$
$\sqrt{23}=4+\sqrt{23}-4=4+\dfrac 1 {\dfrac 1 {\sqrt{23}-4}}=4+\dfrac 1  {1+\dfrac{\sqrt{23}-3}7}$

If we continue we would get the following expansion:

$\sqrt{23}=4+\dfrac 1 {1+\dfrac 1 {3+ \dfrac 1 {1+\dfrac 1 {8+ \dots}}}}$

The process can be summarised as follows:

$a_0=4, \dfrac 1 {\sqrt{23}-4}=\dfrac {\sqrt{23}+4} 7=1+\dfrac {\sqrt{23}-3} 7$<br>
$a_1=1, \dfrac 7 {\sqrt{23}-3}=\dfrac {7(\sqrt{23}+3)} {14}=3+\dfrac {\sqrt{23}-3} 2$<br>
$a_2=3, \dfrac 2 {\sqrt{23}-3}=\dfrac {2(\sqrt{23}+3)} {14}=1+\dfrac {\sqrt{23}-4} 7$<br>
$a_3=1, \dfrac 7 {\sqrt{23}-4}=\dfrac {7(\sqrt{23}+4)} 7=8+\sqrt{23}-4$<br>
$a_4=8, \dfrac 1 {\sqrt{23}-4}=\dfrac {\sqrt{23}+4} 7=1+\dfrac {\sqrt{23}-3} 7$<br>
$a_5=1, \dfrac 7 {\sqrt{23}-3}=\dfrac {7 (\sqrt{23}+3)} {14}=3+\dfrac {\sqrt{23}-3} 2$<br>
$a_6=3, \dfrac 2 {\sqrt{23}-3}=\dfrac {2(\sqrt{23}+3)} {14}=1+\dfrac {\sqrt{23}-4} 7$<br>
$a_7=1, \dfrac 7 {\sqrt{23}-4}=\dfrac {7(\sqrt{23}+4)} {7}=8+\sqrt{23}-4$<br>

It can be seen that the sequence is repeating. For conciseness, we use the notation $\sqrt{23}=[4;(1,3,1,8)]$, to indicate that the block $(1,3,1,8)$ repeats indefinitely.

The first ten continued fraction representations of (irrational) square roots are:

$\sqrt{2}=[1;(2)]$, period=$1$<br>
$\sqrt{3}=[1;(1,2)]$, period=$2$<br>
$\sqrt{5}=[2;(4)]$, period=$1$<br>
$\sqrt{6}=[2;(2,4)]$, period=$2$<br>
$\sqrt{7}=[2;(1,1,1,4)]$, period=$4$<br>
$\sqrt{8}=[2;(1,4)]$, period=$2$<br>
$\sqrt{10}=[3;(6)]$, period=$1$<br>
$\sqrt{11}=[3;(3,6)]$, period=$2$<br>
$\sqrt{12}=[3;(2,6)]$, period=$2$<br>
$\sqrt{13}=[3;(1,1,1,1,6)]$, period=$5$<br>

Exactly four continued fractions, for $N \le 13$, have an odd period.

How many continued fractions for $N \le 10\,000$ have an odd period?

## 解决方案

本题主要以查阅资料等方式得以解决。

该计算[周期性连分数](https://en.wikipedia.org/wiki/Periodic_continued_fraction#Canonical_form_and_repetend)的维基百科页面中，给出了一种计算连分数序列$\{a\}$的递推算法：

$\begin{aligned}
m_0 &=0 \\
d_0 &= 1 \\
a_0&=\lfloor\sqrt {S}\rfloor \\
m_{n+1}&=d_na_n-m_n \\
d_{n+1}&=\dfrac{S-m_{n+1}^2}{d_n}\\
a_{n+1}&=\lfloor\dfrac{a_0+m_{n+1}}{d_{n+1}}\rfloor
\end{aligned}$

其中，$\{m\},\{d\},\{a\}$三个数列都是整数序列。当计算到$a_n=2a_0$时，算法终止迭代，$n$就是周期本身。

依照该维基百科提供的内容，即可完成每个连分数的$\{a\}$序列周期计算。

## 代码

```py
from tools import int_sqrt, is_square

# https://en.wikipedia.org/wiki/Periodic_continued_fraction#Canonical_form_and_repetend
N = 10000
ans = 0
for S in range(2, N + 1):
    if is_square(S):
        continue
    m = 0
    d = 1
    a0 = int_sqrt(S)
    tm = 0
    a = a0
    while a != 2 * a0:
        m = d * a - m
        d = (S - m * m) // d
        a = (a0 + m) // d
        tm += 1
    if tm & 1:
        ans += 1
print(ans)

```
