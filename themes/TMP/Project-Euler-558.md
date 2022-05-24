---
title: Project Euler 558
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 558
## 题目
### Irrational base

Let <var>r</var> be the real root of the equation <var>x</var>^3 = <var>x</var>^2 + 1.<br />
Every positive integer can be written as the sum of distinct increasing powers of <var>r</var>.<br />
If we require the number of terms to be finite and the difference between any two exponents to be three or more, then the representation is unique.<br />
For example, 3 = <var>r</var>^ -10 + <var>r</var>^ -5 + <var>r</var>^ -1 + <var>r</var>^ 2 and 10 = <var>r</var>^ -10 + <var>r</var>^ -7 + <var>r</var>^ 6.<br />
Interestingly, the relation holds for the complex roots of the equation.

Let <var>w</var>(<var>n</var>) be the number of terms in this unique representation of <var>n</var>. Thus <var>w</var>(3) = 4 and <var>w</var>(10) = 3.

More formally, for all positive integers <var>n</var>, we have:<br /><var>n</var> = $\displaystyle \sum_{k=-\infty}^{\infty}$ <var>b_k r^k</var><br />
under the conditions that:<br /><var>b_k</var> is 0 or 1 for all <var>k</var>;<br /><var>b_k</var> + <var>b</var>_<var>k</var>+1 + <var>b</var>_<var>k</var>+2 \le 1 for all <var>k</var>;<br /><var>w</var>(<var>n</var>) = $\displaystyle \sum_{k=-\infty}^{\infty}$ <var>b_k</var> is finite.

Let S(<var>m</var>) = $\displaystyle \sum_{j=1}^{m}$ <var>w</var>(<var>j</var>^2).<br />
You are given S(10) = 61 and S(1000) = 19403.

Find S(5 000 000).



# Project Euler 558
## 题目
### Irrational base

Let r be the real root of the equation x^3=x^2+1.<br>Every positive integer can be written as the sum of distinct increasing powers of r.<br>If we require the number of terms to be finite and the difference between any two exponents to be three or more, then the representation is unique.<br>For example, 3=r^-10+r^-5+r^-1+r^2 and 10=r^-10+r^-7+r^6.<br>Interestingly, the relation holds for the complex roots of the equation.
Let w(n) be the number of terms in this unique representation of n. Thus w(3)=4 and w(10)=3.
More formally, for all positive integers n, we have:<br>n = $\displaystyle \sum_{k=-\infty}^{\infty}$ b_kr^k<br>under the conditions that:<br>b_k is 0 or 1 for all k;<br>b_k+b_k+1+b_k+2\le1 for all k;<br>w(n) = $\displaystyle \sum_{k=-\infty}^{\infty}$ b_k is finite.
Let S(m)= $\displaystyle \sum_{j=1}^{m}$w(j^2).<br>You are given S(10) = 61 and S(1000) = 19403.
Find S(5 000 000).


## 解决方案


## 代码


