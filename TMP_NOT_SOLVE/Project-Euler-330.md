---
title: Project Euler 330
category:
  - Project Euler
tags:
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 330
## 题目
### Euler's Number


An infinite sequence of real numbers <var>a</var>(<var>n</var>) is defined for all integers <var>n</var> as follows:
$$a(n) = \begin{cases}
1 &amp; n \lt 0\\
\sum \limits_{i = 1}^{\infty}{\dfrac{a(n - i)}{i!}} &amp; n \ge 0
\end{cases}$$

For example,<br />

$a(0) = \dfrac{1}{1!} + \dfrac{1}{2!} + \dfrac{1}{3!} + \cdots = e - 1$<br />
$a(1) = \dfrac{e - 1}{1!} + \dfrac{1}{2!} + \dfrac{1}{3!} + \cdots = 2e - 3$<br />
$a(2) = \dfrac{2e - 3}{1!} + \dfrac{e - 1}{2!} + \dfrac{1}{3!} + \cdots = \dfrac{7}{2}e - 6$

with $e = 2.7182818\dots$ being Euler's constant.

It can be shown that $a(n)$ is of the form $\dfrac{A(n)e + B(n)}{n!}$ for integers $A(n)$ and $B(n)$.

For example, $a(10) = \dfrac{328161643e - 652694486}{10!}$.

Find $A(10^9) + B(10^9)$ and give your answer mod 77 777 777.


# Project Euler 330
## 题目
### Euler’s Number

An infinite sequence of real numbers a(n) is defined for all integers n as follows:
<center><img src="https://projecteuler.net/project/images/p330_formula.gif"></center>

For example,<br>a(0)=$\frac{1}{1!}$+$\frac{1}{2!}$+$\frac{1}{3!}$+\dots=e-1<br>a(1)=$\frac{1}{1!}$+$\frac{1}{2!}$+$\frac{1}{3!}$+\dots=e-1<br>a(2)=$\frac{2e-3}{1!}$+$\frac{e-1}{2!}$+$\frac{1}{3!}$+\dots=$\frac{7}{2}$e-6<br>with e = 2.7182818\dots being Euler’s constant.
It can be shown that a(n) is of the form $\frac{A(n)e+B(n)}{n!}$ for integers A(n) and B(n).<br>For example a(10) = $\frac{328161643 e − 652694486}{10!}$.
Find A(10^9) + B(10^9) and give your answer mod 77 777 777.


## 解决方案


## 代码


