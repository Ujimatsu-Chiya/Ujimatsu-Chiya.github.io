---
title: Project Euler 323
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 323
## 题目
### Bitwise-OR operations on random integers

Let <var>y</var>_0, <var>y</var>_1, <var>y</var>_2,\dots be a sequence of random unsigned 32 bit integers<br />
(i.e. 0 \le <var>y_i</var> < 2^32, every value equally likely).
For the sequence <var>x_i</var> the following recursion is given:<br /><ul><li><var>x</var>_0 = 0 and</li>
<li><var>x_i</var> = <var>x</var>_<var>i</var>-<i>1</i><b>|</b> <var>y</var>_<var>i</var>-<i>1</i>, for <var>i</var> > 0. ( <b>|</b> is the bitwise-OR operator)</li>
</ul>It can be seen that eventually there will be an index N such that <var>x_i</var> = 2^32 -1 (a bit-pattern of all ones) for all <var>i</var> \ge N.

Find the expected value of N. <br />
Give your answer rounded to 10 digits after the decimal point.


# Project Euler 323
## 题目
### Bitwise-OR operations on random integers

Let y_0, y_1, y_2,\dots be a sequence of random unsigned 32 bit integers<br>(i.e. 0 \le y_i < 2^32, every value equally likely).
For the sequence x_i the following recursion is given:
<ul>
<li>x_0 = 0 and</li>
<li>x_i = x_i-<i>1</i> **|** y_i-<i>1</i>, for i > 0. ( **|** is the bitwise-OR operator)</li>
</ul>
It can be seen that eventually there will be an index N such that x_i = 2^32 -1 (a bit-pattern of all ones) for all i \ge N.
Find the expected value of N.<br>Give your answer rounded to 10 digits after the decimal point.


## 解决方案


## 代码


