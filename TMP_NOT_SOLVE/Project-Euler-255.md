---
title: Project Euler 255
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 255
## 题目
### Rounded Square Roots

We define the <i>rounded-square-root</i> of a positive integer <var>n</var> as the square root of <var>n</var> rounded to the nearest integer.

The following procedure (essentially Heron's method adapted to integer arithmetic) finds the rounded-square-root of <var>n</var>:
Let <var>d</var> be the number of digits of the number <var>n</var>.<br />
If <var>d</var> is odd, set $x_0 = 2 \times 10^{(d-1)/2}$.<br />
If <var>d</var> is even, set $x_0 = 7 \times 10^{(d-2)/2}$.<br />
Repeat:
$$x_{k+1} = \Biggl\lfloor{\dfrac{x_k + \lceil{n / x_k}\rceil}{2}}\Biggr\rfloor$$

until $x_{k+1} = x_k$.
As an example, let us find the rounded-square-root of <var>n</var> = 4321.<br /><var>n</var> has 4 digits, so $x_0 = 7 \times 10^{(4-2)/2} = 70$.<br />
$$x_1 = \Biggl\lfloor{\dfrac{70 + \lceil{4321 / 70}\rceil}{2}}\Biggr\rfloor = 66$$
$$x_2 = \Biggl\lfloor{\dfrac{66 + \lceil{4321 / 66}\rceil}{2}}\Biggr\rfloor = 66$$

Since $x_2 = x_1$, we stop here.<br />
So, after just two iterations, we have found that the rounded-square-root of 4321 is 66 (the actual square root is 65.7343137\dots).

The number of iterations required when using this method is surprisingly low.<br />
For example, we can find the rounded-square-root of a 5-digit integer (10,000 \le <var>n</var> \le 99,999) with an average of 3.2102888889 iterations (the average value was rounded to 10 decimal places).

Using the procedure described above, what is the average number of iterations required to find the rounded-square-root of a 14-digit number (10^13 \le <var>n</var> < 10^14)?<br />
Give your answer rounded to 10 decimal places.

Note: The symbols $\lfloor x \rfloor$ and $\lceil x \rceil$ represent the <dfn title="the largest integer not greater than x">floor function</dfn> and <dfn title="the smallest integer not less than x">ceiling function</dfn> respectively.



# Project Euler 255
## 题目
### Rounded Square Roots

We define the <em>rounded-square-root</em> of a positive integer n as the square root of n rounded to the nearest integer.
The following procedure (essentially Heron’s method adapted to integer arithmetic) finds the rounded-square-root of n:
Let d be the number of digits of the number n.<br>If d is odd, set x_0 = 2\times10^(d-1)⁄2.<br>If d is even, set x_0 = 7\times10^(d-2)⁄2.<br>Repeat:
<center><img src="https://projecteuler.net/project/images/p255_Heron.gif"></center>

until x_k+1 = x_k.
As an example, let us find the rounded-square-root of n = 4321.<br>n has 4 digits, so x_0 = 7\times10^(4-2)⁄2 = 70.
<center><img src="https://projecteuler.net/project/images/p255_Example.gif"></center>

Since x_2 = x_1, we stop here.<br>So, after just two iterations, we have found that the rounded-square-root of 4321 is 66 (the actual square root is 65.7343137\dots).
The number of iterations required when using this method is surprisingly low.<br>For example, we can find the rounded-square-root of a 5-digit integer (10,000 \le n \le 99,999) with an average of 3.2102888889 iterations (the average value was rounded to 10 decimal places).
Using the procedure described above, what is the average number of iterations required to find the rounded-square-root of a 14-digit number (10^13 \le n < 10^14)?<br>Give your answer rounded to 10 decimal places.
Note: The symbols ⌊x⌋ and ⌈x⌉ represent the <dfn title="the largest integer not greater than x">floor function</dfn> and <dfn title="the smallest integer not less than x">ceiling function</dfn> respectively.


## 解决方案


## 代码


