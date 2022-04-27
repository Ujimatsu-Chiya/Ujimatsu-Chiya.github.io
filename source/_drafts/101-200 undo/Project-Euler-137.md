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

<table class="p236" cellpadding="0" cellspacing="0" border="0"><tr><td valign="top">Surprisingly</td><td>$\begin{align*} 
A_F(\tfrac{1}{2})
 &amp;= (\tfrac{1}{2})\times 1 + (\tfrac{1}{2})^2\times 1 + (\tfrac{1}{2})^3\times 2 + (\tfrac{1}{2})^4\times 3 + (\tfrac{1}{2})^5\times 5 + \cdots \\ 
 &amp;= \tfrac{1}{2} + \tfrac{1}{4} + \tfrac{2}{8} + \tfrac{3}{16} + \tfrac{5}{32} + \cdots \\
 &amp;= 2
\end{align*}$</td>
</tr></table>The corresponding values of <i>x</i> for the first five natural numbers are shown below.
<div class="center">
<table cellspacing="0" cellpadding="2" border="1" align="center"><tr><th>$x$</th><th width="50">$A_F(x)$</th>
</tr><tr><td>$\sqrt{2}-1$</td><td>1</td>
</tr><tr><td>$\tfrac{1}{2}$</td><td>2</td>
</tr><tr><td>$\frac{\sqrt{13}-2}{3}$</td><td>3</td>
</tr><tr><td>$\frac{\sqrt{89}-5}{8}$</td><td>4</td>
</tr><tr><td>$\frac{\sqrt{34}-3}{5}$</td><td>5</td>
</tr></table>

# Project Euler 137
## 题目
### Fibonacci golden nuggets
Consider the infinite polynomial series A_F(x) = xF_1 + x^2F_2 + x^3F_3 + \dots, where F_k is the kth term in the Fibonacci sequence: 1, 1, 2, 3, 5, 8, \dots ; that is, F_k = F_k−1 + F_k−2, F_1 = 1 and F_2 = 1.
For this problem we shall be interested in values of x for which A_F(x) is a positive integer.
Surprisingly
<table>
<thead>
<tr>
<th align="right">&nbsp;</th>
<th align="center">&nbsp;</th>
<th align="left">&nbsp;</th>
</tr>
</thead>
<tbody><tr>
<td align="right">A_F(1/2)</td>
<td align="center">=</td>
<td align="left">(1/2).1 + (1/2)^2.1 + (1/2)^3.2 + (1/2)^4.3 + (1/2)^5.5 + \dots</td>
</tr>
<tr>
<td align="right">&nbsp;</td>
<td align="center">=</td>
<td align="left">1/2 + 1/4 + 2/8 + 3/16 + 5/32 + \dots</td>
</tr>
<tr>
<td align="right">&nbsp;</td>
<td align="center">=</td>
<td align="left">2</td>
</tr>
</tbody></table>
The corresponding values of x for the first five natural numbers are shown below.
<table>
<thead>
<tr>
<th align="center">**x**</th>
<th align="center">**A_F(x)**</th>
</tr>
</thead>
<tbody><tr>
<td align="center">√2−1</td>
<td align="center">1</td>
</tr>
<tr>
<td align="center">1/2</td>
<td align="center">2</td>
</tr>
<tr>
<td align="center">(√13−2)/3</td>
<td align="center">3</td>
</tr>
<tr>
<td align="center">(√89−5)/8</td>
<td align="center">4</td>
</tr>
<tr>
<td align="center">(√34−3)/5</td>
<td align="center">5</td>
</tr>
</tbody></table>
We shall call A_F(x) a golden nugget if x is rational, because they become increasingly rarer; for example, the 10th golden nugget is 74049690.
Find the 15th golden nugget.


## 解决方案


## 代码


