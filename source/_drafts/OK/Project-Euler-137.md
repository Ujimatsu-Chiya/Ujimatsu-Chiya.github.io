---
title: Project Euler 137
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 137
## 题目
### Fibonacci golden nuggets


Consider the infinite polynomial series $A_F(x) = x F_1 + x^2 F_2 + x^3 F_3 + \dots$, where $F_k$ is the $k$th term in the Fibonacci sequence: $1, 1, 2, 3, 5, 8, \dots$; that is, $F_k = F_{k-1} + F_{k-2}$, $F_1 = 1$ and $F_2 = 1$.

For this problem we shall be interested in values of $x$ for which $A_F(x)$ is a positive integer.

Surprisingly 
$\begin{aligned} 
A_F(\tfrac{1}{2})
 & = (\tfrac{1}{2})\times 1 + (\tfrac{1}{2})^2\times 1 + (\tfrac{1}{2})^3\times 2 + (\tfrac{1}{2})^4\times 3 + (\tfrac{1}{2})^5\times 5 + \cdots \\ 
 & = \tfrac{1}{2} + \tfrac{1}{4} + \tfrac{2}{8} + \tfrac{3}{16} + \tfrac{5}{32} + \cdots \\
 & = 2
\end{aligned}$

The corresponding values of $x$ for the first five natural numbers are shown below.

|$x$|$A_F(x)$|
|-|-|
|$\sqrt{2}-1$|$1$|
|$\dfrac{1}{2}$|$2$|
|$\dfrac{\sqrt{13}-2}{3}$|$3$|
|$\dfrac{\sqrt{89}-5}{8}$|$4$|
|$\dfrac{\sqrt{34}-3}{5}$|$5$|

We shall call $A_F(x)$ a golden nugget if $x$ is rational, because they become increasingly rarer; for example, the $10\mathrm{th}$ golden nugget is $74049690$.

Find the $15\mathrm{th}$ golden nugget.


## 解决方案


## 代码


