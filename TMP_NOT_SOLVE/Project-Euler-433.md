---
title: Project Euler 433
category:
  - Project Euler
tags:
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 433
## 题目
### Steps in Euclid's algorithm



Let E(<var>x</var>_0, <var>y</var>_0) be the number of steps it takes to determine the greatest common divisor of <var>x</var>_0 and <var>y</var>_0 with <b>Euclid's algorithm</b>. More formally:<br /><var>x</var>_1 = <var>y</var>_0, <var>y</var>_1 = <var>x</var>_0 mod <var>y</var>_0<br /><var>x_n</var> = <var>y</var>_<var>n</var>-1, <var>y</var>_<var>n</var> = <var>x</var>_<var>n</var>-1 mod <var>y</var>_<var>n</var>-1<br />
E(<var>x</var>_0, <var>y</var>_0) is the smallest <var>n</var> such that <var>y</var>_<var>n</var> = 0.


We have E(1,1) = 1, E(10,6) = 3 and E(6,10) = 4.


Define S(N) as the sum of E(<var>x,y</var>) for 1 \le <var>x,y</var> \le N.<br />
We have S(1) = 1, S(10) = 221 and S(100) = 39826.


Find S(5·10^6).





# Project Euler 433
## 题目
### Steps in Euclid’s algorithm

Let E(x_0, y_0) be the number of steps it takes to determine the greatest common divisor of x_0 and y_0 with **Euclid’s algorithm**. More formally:<br>x_1 = y_0, y_1 = x_0 mod y_0<br>x_n = y_n-1, y_n = x_n-1 mod y_n-1<br>E(x_0, y_0) is the smallest n such that y_n = 0.
We have E(1,1) = 1, E(10,6) = 3 and E(6,10) = 4.
Define S(N) as the sum of E(x,y) for 1 \le x,y \le N.<br>We have S(1) = 1, S(10) = 221 and S(100) = 39826.
Find S(5·10^6).


## 解决方案


## 代码


