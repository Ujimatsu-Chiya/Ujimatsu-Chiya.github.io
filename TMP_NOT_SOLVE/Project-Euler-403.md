---
title: Project Euler 403
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 403
## 题目
### Lattice points enclosed by parabola and line


For integers <var>a</var> and <var>b</var>, we define <var>D</var>(<var>a</var>, <var>b</var>) as the domain enclosed by the parabola <var>y</var> = <var>x</var>^2 and the line <var>y</var> = <var>a</var>·<var>x</var> + <var>b</var>:<br /><var>D</var>(<var>a</var>, <var>b</var>) = { (<var>x</var>, <var>y</var>) | <var>x</var>^2 \le <var>y</var> \le <var>a</var>·<var>x</var> + <var>b</var> }.


L(<var>a</var>, <var>b</var>) is defined as the number of lattice points contained in <var>D</var>(<var>a</var>, <var>b</var>).<br />
For example, L(1, 2) = 8 and L(2, -1) = 1.


We also define S(<var>N</var>) as the sum of L(<var>a</var>, <var>b</var>) for all the pairs (<var>a</var>, <var>b</var>) such that the area of <var>D</var>(<var>a</var>, <var>b</var>) is a rational number and |<var>a</var>|,|<var>b</var>| \le <var>N</var>.<br />
We can verify that S(5) = 344 and S(100) = 26709528.


Find S(10^12). Give your answer mod 10^8.



# Project Euler 403
## 题目
### Lattice points enclosed by parabola and line

For integers a and b, we define D(a, b) as the domain enclosed by the parabola y = x^2 and the line y = a·x + b:<br>D(a, b) = { (x, y) | x^2 \le y \le a·x + b }.
L(a, b) is defined as the number of lattice points contained in D(a, b).<br>For example, L(1, 2) = 8 and L(2, -1) = 1.
We also define S(N) as the sum of L(a, b) for all the pairs (a, b) such that the area of D(a, b) is a rational number and |a|,|b| \le N.<br>We can verify that S(5) = 344 and S(100) = 26709528.
Find S(10^12). Give your answer mod 10^8.


## 解决方案


## 代码


