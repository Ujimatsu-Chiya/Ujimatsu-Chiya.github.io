---
title: Project Euler 471
category:
  - Project Euler
tags:
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 471
## 题目
### Triangle inscribed in ellipse


The triangle ΔABC is inscribed in an ellipse with equation $\frac {x^2} {a^2} + \frac {y^2} {b^2} = 1$, 0 < 2<var>b</var> < <var>a</var>, <var>a</var> and <var>b</var> integers.
Let <var>r</var>(<var>a</var>,<var>b</var>) be the radius of the incircle of ΔABC when the incircle has center (2<var>b</var>, 0) and A has coordinates $\left( \frac a 2, \frac {\sqrt 3} 2 b\right)$.
For example, <var>r</var>(3,1) = ½, <var>r</var>(6,2) = 1, <var>r</var>(12,3) = 2.
<p align="center"><img src="project/images/p471-triangle-inscribed-in-ellipse-1.png" alt="p471-triangle-inscribed-in-ellipse-1.png" />
<p align="center"><img src="project/images/p471-triangle-inscribed-in-ellipse-2.png" alt="p471-triangle-inscribed-in-ellipse-2.png" />
Let $G(n) = \sum_{a=3}^n \sum_{b=1}^{\lfloor \frac {a - 1} 2 \rfloor} r(a, b)$
You are given <var>G</var>(10) = 20.59722222, <var>G</var>(100) = 19223.60980 (rounded to 10 significant digits).
Find <var>G</var>(10^11).
Give your answer in scientific notation rounded to 10 significant digits. Use a lowercase e to separate mantissa and exponent.
For <var>G</var>(10) the answer would have been 2.059722222e1.


# Project Euler 471
## 题目
### Triangle inscribed in ellipse

The triangle ΔABC is inscribed in an ellipse with equation $\frac{x^2}{a^2}+\frac{y^2}{b^2}=1$, 0 < 2b < a, a and b integers.
Let r(a,b) be the radius of the incircle of ΔABC when the incircle has center (2b, 0) and A has coordinates $(\frac{a}{2}, \frac{\sqrt{3}}{2}b)$.
For example, r(3,1) = ½, r(6,2) = 1, r(12,3) = 2.
<center><img src="https://projecteuler.net/project/images/p471-triangle-inscribed-in-ellipse-1.png"></center>
<center><img src="https://projecteuler.net/project/images/p471-triangle-inscribed-in-ellipse-2.png"></center>

Let $G(n)=\sum_{a=3}^{n}\sum_{b=1}^{\lfloor \frac{a-1}{2} \rfloor}r(a,b)$
You are given G(10) = 20.59722222, G(100) = 19223.60980 (rounded to 10 significant digits).
Find G(1011).
Give your answer in scientific notation rounded to 10 significant digits. Use a lowercase e to separate mantissa and exponent.
For G(10) the answer would have been 2.059722222e1.


## 解决方案


## 代码


