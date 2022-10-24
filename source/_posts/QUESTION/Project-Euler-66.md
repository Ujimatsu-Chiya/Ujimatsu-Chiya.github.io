---
title: Project Euler 66
category:
  - Project Euler
tags:
  - 佩尔方程
mathjax: true
date: 2022-05-03 09:22:21
---

<escape><!-- more --></escape>

# Project Euler 66

## 题目

### Diophantine equation

Consider quadratic Diophantine equations of the form:

$$x^2 – Dy^2 = 1$$

For example, when $D=13$, the minimal solution in $x$ is $649^2 – 13×180^2 = 1$.

It can be assumed that there are no solutions in positive integers when D is square.

By finding minimal solutions in $x$ for $D = \{2, 3, 5, 6, 7\}$, we obtain the following:

$$\begin{aligned}
3^2 – 2×2^2 = 1 \\
2^2 – 3×1^2 = 1 \\
9^2 – 5×4^2 = 1 \\
5^2 – 6×2^2 = 1 \\
8^2 – 7×3^2 = 1 \\
\end{aligned}$$

Hence, by considering minimal solutions in $x$ for $D \leq 7$, the largest $x$ is obtained when $D=5$.

Find the value of $D \leq 1000$ in minimal solutions of $x$ for which the largest value of $x$ is obtained.

## 解决方案

mathworld wolfram上介绍的关于[佩尔方程](https://mathworld.wolfram.com/PellEquation.html)$x^2-Dy^2=1$的一组特解的解法基于连分数解决（此处假设$D$为非平方整数）。

设$\sqrt{N}$产生的连分数序列表示成$[a_0;(a_1,a_2,\dots,a_n)]$，其中$a_n=2a_0$。

那么计算$\sqrt{N}$的连分数序列算法已在64题中的提到的维基百科页面给出：

$\begin{aligned}
m_0 &=0 \\
d_0 &= 1 \\
a_0&=\lfloor\sqrt {S}\rfloor \\
m_{n+1}&=d_na_n-m_n \\
d_{n+1}&=\dfrac{S-m_{n+1}^2}{d_n}\\
a_{n+1}&=\left\lfloor\dfrac{a_0+m_{n+1}}{d_{n+1}}\right\rfloor
\end{aligned}$

网站上提到，为计算$x^2-Dy^2=1$，假设$\sqrt{N}$产生的第$m$个连分数$[a_0,a_1,\dots,a_m]$的分数形式为$\dfrac{p_m}{q_m}$。

那么如果连分数周期$n$为偶数，$x^2-Dy^2=1$的最小特解为$(p_{n-1},q_{n-1})$。

否则，$x^2-Dy^2=1$的最小特解为$(p_{2n-1},q_{2n-1})$。

直接使用这一些结论进行计算。

另外，假设该最小特解为$(x_1,y_1)$，那么佩尔方程的通解$(x_k,y_k)$可以由以下结果导出：

$$x_k+y_k\sqrt{D}=(x_1+y_1\sqrt{D})^k$$

即有关于$(x_k,y_k)$两个序列的递推式：
$$
\left \{\begin{aligned}
  & x_{k+1}=x_1x_k+Dy_1y_k\\
  & y_{k+1}=x_1y_k+y_1x_k
\end{aligned}\right.
$$

## 代码

```py
from fractions import Fraction
from tools import int_sqrt, is_square

N = 1000
ans, mx = 0, 0
for D in range(1, N + 1):
    if is_square(D):
        continue
    m = 0
    d = 1
    a0 = int(int_sqrt(D))
    ls = [a0]
    a = a0
    tm = 0
    while a != 2 * a0:
        m = d * a - m
        d = (D - m * m) // d
        a = (a0 + m) // d
        tm += 1
        ls.append(a)
    if tm % 2 == 0:
        t = ls[:-1][::-1]
    else:
        t = (ls + ls[1:-1])[::-1]
    w = Fraction(t[0])
    for i in range(1, len(t)):
        w = 1 / w + t[i]
    x, y = w.numerator, w.denominator
    if x > mx:
        mx = x
        ans = D
print(ans)

```
