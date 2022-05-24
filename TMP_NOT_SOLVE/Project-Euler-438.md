---
title: Project Euler 438
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 438
## 题目
### Integer part of polynomial equation's solutions


For an <var>n</var>-tuple of integers <var>t</var> = (<var>a</var>_1, \dots, <var>a</var>_<var>n</var>), let (<var>x</var>_1, \dots, <var>x</var>_<var>n</var>) be the solutions of the polynomial equation <var>x</var>^<var>n</var> + <var>a</var>_1<var>x</var>^<var>n</var>-1 + <var>a</var>_2<var>x</var>^<var>n</var>-2 + \dots + <var>a</var>_<var>n</var>-1<var>x</var> + <var>a</var>_<var>n</var> = 0.


Consider the following two conditions:
<ul><li><var>x</var>_1, \dots, <var>x</var>_<var>n</var> are all real.
</li><li>If <var>x</var>_1, \dots, <var>x</var>_<var>n</var> are sorted, ⌊<var>x</var>_<var>i</var>⌋ = <var>i</var> for 1 \le <var>i</var> \le <var>n</var>. (⌊·⌋: floor function.)
</li></ul>
In the case of <var>n</var> = 4, there are 12 <var>n</var>-tuples of integers which satisfy both conditions.<br />
We define S(<var>t</var>) as the sum of the absolute values of the integers in <var>t</var>.<br />
For <var>n</var> = 4 we can verify that <span style="font-size:larger;"><span style="font-size:larger;">\sum</span></span> S(<var>t</var>) = 2087 for all <var>n</var>-tuples <var>t</var> which satisfy both conditions.


Find <span style="font-size:larger;"><span style="font-size:larger;">\sum</span></span> S(<var>t</var>) for <var>n</var> = 7.



# Project Euler 438
## 题目
### Integer part of polynomial equation’s solutions

For an n-tuple of integers t = (a_1, \dots, a_n), let (x_1, \dots, x_n) be the solutions of the polynomial equation x^n + a_1x^n-1 + a_2x^n-2 + \dots + a_n-1x + a_n = 0.
Consider the following two conditions:
<ul>
<li>x_1, \dots, x_n are all real.</li>
<li>If x_1, \dots, x_n are sorted, [x_i] = i for 1 \le i \le n. ([·]: floor function.)</li>
</ul>
In the case of n = 4, there are 12 n-tuples of integers which satisfy both conditions.<br>We define S(t) as the sum of the absolute values of the integers in t.<br>For n = 4 we can verify that \sumS(t) = 2087 for all n-tuples t which satisfy both conditions.
Find \sumS(t) for n = 7.


## 解决方案


## 代码


