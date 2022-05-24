---
title: Project Euler 545
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 545
## 题目
### Faulhaber's Formulas

The sum of the <var>k</var>^th powers of the first <var>n</var> positive integers can be expressed as a polynomial of degree <var>k</var>+1 with rational coefficients, the <b>Faulhaber's Formulas</b>:<br />
$1^k + 2^k + \dots + n^k = \sum_{i=1}^n i^k = \sum_{i=1}^{k+1} a_{i} n^i = a_{1} n + a_{2} n^2 + \dots + a_{k} n^k + a_{k+1} n^{k + 1}$,<br />
where <var>a_i</var>'s are rational coefficients that can be written as reduced fractions <var>p_i</var>/<var>q_i</var> (if <var>a_i</var> = 0, we shall consider <var>q_i</var> = 1).

For example, $1^4 + 2^4 + \dots + n^4 = -\frac 1 {30} n + \frac 1 3 n^3 + \frac 1 2 n^4 + \frac 1 5 n^5.$

Define D(<var>k</var>) as the value of <var>q</var>_1 for the sum of <var>k</var>^th powers (i.e. the denominator of the reduced fraction <var>a</var>_1).<br />
Define F(<var>m</var>) as the <var>m</var>^th value of <var>k</var> \ge 1 for which D(<var>k</var>) = 20010.<br />
You are given D(4) = 30 (since <var>a</var>_1 = -1/30), D(308) = 20010, F(1) = 308, F(10) = 96404.

Find F(10^5).


# Project Euler 545
## 题目
### Faulhaber’s Formulas

The sum of the k^th powers of the first n positive integers can be expressed as a polynomial of degree k+1 with rational coefficients, the <b>Faulhaber’s Formulas</b>:<br>$$1^k + 2^k + \dots + n^k = \sum_{i=1}^n i^k = \sum_{i=1}^{k+1} a_{i} n^i = a_{1} n + a_{2} n^2 + \dots + a_{k} n^k + a_{k+1} n^{k + 1},$$<br>where a_i‘s are rational coefficients that can be written as reduced fractions p_i/q_i (if a_i&nbsp;=&nbsp;0, we shall consider q_i&nbsp;=&nbsp;1).
For example, $1^4 + 2^4 + \dots + n^4 = -\frac{1}{30}n + \frac{1}{3}n^3 + \frac{1}{2}n^4 + \frac{1}{5}n^5$.
Define D(k) as the value of q_1 for the sum of k^th powers (i.e. the denominator of the reduced fraction a_1).<br>Define F(m) as the m^th value of k&nbsp;\ge&nbsp;1 for which D(k)&nbsp;=&nbsp;20010.<br>You are given D(4) = 30 (since a_1&nbsp;=&nbsp;-1/30), D(308)&nbsp;=&nbsp;20010, F(1)&nbsp;=&nbsp;308, F(10)&nbsp;=&nbsp;96404.
Find F(10^5).


## 解决方案


## 代码


