---
title: Project Euler 402
category:
  - Project Euler
tags:
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 402
## 题目
### Integer-valued polynomials



It can be shown that the polynomial <var>n</var>^4 + 4<var>n</var>^3 + 2<var>n</var>^2 + 5<var>n</var> is a multiple of 6 for every integer <var>n</var>. It can also be shown that 6 is the largest integer satisfying this property.


Define M(<var>a</var>, <var>b</var>, <var>c</var>) as the maximum <var>m</var> such that <var>n</var>^4 + <var>a</var><var>n</var>^3 + <var>b</var><var>n</var>^2 + <var>c</var><var>n</var> is a multiple of <var>m</var> for all integers <var>n</var>. For example, M(4, 2, 5) = 6.


Also, define S(<var>N</var>) as the sum of M(<var>a</var>, <var>b</var>, <var>c</var>) for all 0 < <var>a</var>, <var>b</var>, <var>c</var> \le <var>N</var>.


We can verify that S(10) = 1972 and S(10000) = 2024258331114.


Let F_<var>k</var> be the Fibonacci sequence:<br />
F_0 = 0, F_1 = 1 and<br />
F_<var>k</var> = F_<var>k</var>-1 + F_<var>k</var>-2 for <var>k</var> \ge 2.


Find the last 9 digits of <span style="font-size:larger;"><span style="font-size:larger;">\sum</span></span> S(F_<var>k</var>) for 2 \le <var>k</var> \le 1234567890123.



# Project Euler 402
## 题目
### Integer-valued polynomials

It can be shown that the polynomial n^4 + 4n^3 + 2n^2 + 5n is a multiple of 6 for every integer n. It can also be shown that 6 is the largest integer satisfying this property.
Define M(a, b, c) as the maximum m such that n^4 + an^3 + bn^2 + cn is a multiple of m for all integers n. For example, M(4, 2, 5) = 6.
Also, define S(N) as the sum of M(a, b, c) for all 0 < a, b, c \le N.
We can verify that S(10) = 1972 and S(10000) = 2024258331114.
Let F_k be the Fibonacci sequence:<br>F_0 = 0, F_1 = 1 and<br>F_k = F_k-1 + F_k-2 for k \ge 2.
Find the last 9 digits of \sum S(F_k) for 2 \le k \le 1234567890123.


## 解决方案


## 代码


