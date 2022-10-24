---
title: Project Euler 547
category:
  - Project Euler
tags:
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 547
## 题目
### Distance of random points within hollow square laminae


Assuming that two points are chosen randomly (with <b>uniform distribution</b>) within a rectangle, it is possible to determine the <b>expected value</b> of the distance between these two points.

For example, the expected distance between two random points in a unit square is about 0.521405, while the expected distance between two random points in a rectangle with side lengths 2 and 3 is about 1.317067.

Now we define a <i>hollow square lamina</i> of size <var>n</var> to be an integer sized square with side length <var>n</var> \ge 3 consisting of <var>n</var>^2 unit squares from which a rectangle consisting of <var>x</var> \times <var>y</var> unit squares (1 \le <var>x</var>,<var>y</var> \le <var>n</var> - 2) within the original square has been removed.

For <var>n</var> = 3 there exists only one hollow square lamina:

<p align="center"><img src="project/images/p547-holes-1.png" alt="p547-holes-1.png" />

For <var>n</var> = 4 you can find 9 distinct hollow square laminae, allowing shapes to reappear in rotated or mirrored form:

<p align="center"><img src="project/images/p547-holes-2.png" alt="p547-holes-2.png" />

Let S(<var>n</var>) be the sum of the expected distance between two points chosen randomly within each of the possible hollow square laminae of size <var>n</var>. The two points have to lie within the area left after removing the inner rectangle, i.e. the gray-colored areas in the illustrations above.

For example, S(3) = 1.6514 and S(4) = 19.6564, rounded to four digits after the decimal point.

Find S(40) rounded to four digits after the decimal point.


# Project Euler 547
## 题目
### Distance of random points within hollow square laminae

Assuming that two points are chosen randomly (with <b>uniform distribution</b>) within a rectangle, it is possible to determine the <b>expected value</b> of the distance between these two points.
For example, the expected distance between two random points in a unit square is about 0.521405, while the expected distance between two random points in a rectangle with side lengths 2 and 3 is about 1.317067.
Now we define a <i>hollow square lamina</i> of size n to be an integer sized square with side length n \ge 3 consisting of n^2 unit squares from which a rectangle consisting of x \times y unit squares (1 \le x,y \le n - 2) within the original square has been removed.
For n = 3 there exits only one hollow square lamina:
<center><img src="https://projecteuler.net/project/images/p547-holes-1.png" alt="p547-holes-1.png"></center>

For n = 4 you can find 9 distinct hollow square laminae, allowing shapes to reappear in rotated or mirrored form:
<center><img src="https://projecteuler.net/project/images/p547-holes-2.png" alt="p547-holes-2.png"></center>

Let S(n) be the sum of the expected distance between two points chosen randomly within each of the possible hollow square laminae of size n. The two points have to lie within the area left after removing the inner rectangle, i.e. the gray-colored areas in the illustrations above.
For example, S(3) = 1.6514 and S(4) = 19.6564, rounded to four digits after the decimal point.
Find S(40) rounded to four digits after the decimal point.


## 解决方案


## 代码


