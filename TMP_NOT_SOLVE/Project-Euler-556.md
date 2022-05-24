---
title: Project Euler 556
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 556
## 题目
### Squarefree Gaussian Integers

A <b>Gaussian integer</b> is a number <var>z</var> = <var>a</var> + <var>b</var>i where <var>a</var>, <var>b</var> are integers and i^2 = -1.<br />
Gaussian integers are a subset of the complex numbers, and the integers are the subset of Gaussian integers for which <var>b</var> = 0.

A Gaussian integer <b>unit</b> is one for which <var>a</var>^2 + <var>b</var>^2 = 1, i.e. one of 1, i, -1, -i.<br />
Let's define a <i>proper</i> Gaussian integer as one for which <var>a</var> > 0 and <var>b</var> \ge 0.

A Gaussian integer z_1 = a_1 + <var>b</var>_1i is said to be divisible by <var>z</var>_2 = a_2 + <var>b</var>_2i if <var>z</var>_3 = <var>a</var>_3 + <var>b</var>_3i = <var>z</var>_1/<var>z</var>_2 is a Gaussian integer.<br />
$\frac {z_1} {z_2} = \frac {a_1 + b_1 i} {a_2 + b_2 i} = \frac {(a_1 + b_1 i)(a_2 - b_2 i)} {(a_2 + b_2 i)(a_2 - b_2 i)} = \frac {a_1 a_2 + b_1 b_2} {a_2^2 + b_2^2} + \frac  {a_2 b_1 - a_1 b_2}  {a_2^2 + b_2^2}i = a_3 + b_3 i$<br />
So, <var>z</var>_1 is divisible by <var>z</var>_2 if $\frac {a_1 a_2 + b_1 b_2} {a_2^2 + b_2^2}$ and $\frac  {a_2 b_1 - a_1 b_2}  {a_2^2 + b_2^2}$ are integers.<br />
For example, 2 is divisible by 1 + i because 2/(1 + i) = 1 - i is a Gaussian integer.

A <b>Gaussian prime</b> is a Gaussian integer that is divisible only by a unit, itself or itself times a unit.<br />
For example, 1 + 2i is a Gaussian prime, because it is only divisible by 1, i, -1, -i, 1 + 2i, i(1 + 2i) = i - 2, -(1 + 2i) = -1 - 2i and -i(1 + 2i) = 2 - i.<br />
2 is not a Gaussian prime as it is divisible by 1 + i.

A Gaussian integer can be uniquely factored as the product of a unit and proper Gaussian primes.<br />
For example 2 = -i(1 + i)^2 and 1 + 3i = (1 + i)(2 + i).<br />
A Gaussian integer is said to be squarefree if its prime factorization does not contain repeated proper Gaussian primes.<br />
So 2 is not squarefree over the Gaussian integers, but 1 + 3i is.<br />
Units and Gaussian primes are squarefree by definition.

Let <var>f</var>(<var>n</var>) be the count of proper squarefree Gaussian integers with <var>a</var>^2 + <var>b</var>^2 \le n.<br />
For example <var>f</var>(10) = 7 because 1, 1 + i, 1 + 2i, 1 + 3i = (1 + i)(2 + i), 2 + i, 3 and 3 + i = -i(1 + i)(1 + 2i) are squarefree, while 2 = -i(1 + i)^2 and 2 + 2i = -i(1 + i)^3 are not.<br />
You are given <var>f</var>(10^2) = 54, <var>f</var>(10^4) = 5218 and <var>f</var>(10^8) = 52126906.

Find <var>f</var>(10^14).



# Project Euler 556
## 题目
### Squarefree Gaussian Integers

A <b>Gaussian integer</b> is a number z = a + bi where a, b are integers and i^2 = -1.<br>Gaussian integers are a subset of the complex numbers, and the integers are the subset of Gaussian integers for which b = 0.
A Gaussian integer <b>unit</b> is one for which a^2 + b^2 = 1, i.e. one of 1, i, -1, -i.<br>Let’s define a <i>proper</i> Gaussian integer as one for which a > 0 and b \ge 0.
A Gaussian integer z_1 = a_1 + b_1i is said to be divisible by z_2 = a_2 + b_2i if z_3 = a_3 + b_3i = z_1/z_2 is a Gaussian integer.<br>$$\frac {z_1} {z_2} = \frac {a_1 + b_1 i} {a_2 + b_2 i} = \frac {(a_1 + b_1 i)(a_2 - b_2 i)} {(a_2 + b_2 i)(a_2 - b_2 i)} = \frac {a_1 a_2 + b_1 b_2} {a_2^2 + b_2^2} + \frac  {a_2 b_1 - a_1 b_2}  {a_2^2 + b_2^2}i = a_3 + b_3 i$$<br>So, z_1 is divisible by z_2 if $\frac {a_1 a_2 + b_1 b_2} {a_2^2 + b_2^2}$ and $\frac  {a_2 b_1 - a_1 b_2}  {a_2^2 + b_2^2}$ are integers.<br>For example, 2 is divisible by 1 + i because 2/(1 + i) = 1 - i is a Gaussian integer.
A <b>Gaussian prime</b> is a Gaussian integer that is divisible only by a unit, itself or itself times a unit.<br>For example, 1 + 2i is a Gaussian prime, because it is only divisible by 1, i, -1, -i, 1 + 2i, i(1 + 2i) = i - 2, -(1 + 2i) = -1 - 2i and -i(1 + 2i) = 2 - i.<br>2 is not a Gaussian prime as it is divisible by 1 + i.
A Gaussian integer can be uniquely factored as the product of a unit and proper Gaussian primes.<br>For example 2 = -i(1 + i)^2 and 1 + 3i = (1 + i)(2 + i).<br>A Gaussian integer is said to be squarefree if its prime factorization does not contain repeated proper Gaussian primes.<br>So 2 is not squarefree over the Gaussian integers, but 1 + 3i is.<br>Units and Gaussian primes are squarefree by definition.
Let f(n) be the count of proper squarefree Gaussian integers with a^2 + b^2 \le n.<br>For example f(10) = 7 because 1, 1 + i, 1 + 2i, 1 + 3i = (1 + i)(2 + i), 2 + i, 3 and 3 + i = -i(1 + i)(1 + 2i) are squarefree, while 2 = -i(1 + i)^2 and 2 + 2i = -i(1 + i)^3 are not.<br>You are given f(10^2) = 54, f(10^4) = 5218 and f(10^8) = 52126906.
Find f(10^14).


## 解决方案


## 代码


