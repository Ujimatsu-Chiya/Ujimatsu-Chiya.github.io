---
title: Project Euler 492
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 492
## 题目
### Exploding sequence

Define the sequence a_1, a_2, a_3, \dots as:
<ul><li>a_1 = 1</li>
<li>a_<var>n</var>+1 = 6a_<var>n</var>^2 + 10a_<var>n</var> + 3 for <var>n</var> \ge 1.</li>
</ul>
Examples:<br />
a_3 = 2359<br />
a_6 = 269221280981320216750489044576319<br />
a_6 mod 1 000 000 007 = 203064689<br />
a_100 mod 1 000 000 007 = 456482974



Define B(<var>x</var>,<var>y</var>,<var>n</var>) as \sum (a_<var>n</var> mod <var>p</var>) for every prime <var>p</var> such that <var>x</var> \le <var>p</var> \le <var>x</var>+<var>y</var>.



Examples:<br />
B(10^9, 10^3, 10^3) = 23674718882<br />
B(10^9, 10^3, 10^15) = 20731563854


Find B(10^9, 10^7, 10^15).



# Project Euler 492
## 题目
### Exploding sequence

Define the sequence a_1, a_2, a_3, \dots as:
<ul>
<li>a_1 = 1</li>
<li>a_n+1 = 6a_n^2 + 10a_n + 3 for n \ge 1.</li>
</ul>
Examples:<br>a_3 = 2359<br>a_6 = 269221280981320216750489044576319<br>a_6 mod 1&nbsp;000&nbsp;000&nbsp;007 = 203064689<br>a_100 mod 1&nbsp;000&nbsp;000&nbsp;007 = 456482974
Define B(x,y,n) as \sum (a_n mod p) for every prime p such that x \le p \le x+y.
Examples:<br>B(10^9, 10^3, 10^3) = 23674718882<br>B(10^9, 10^3, 10^15) = 20731563854
Find B(10^9, 10^7, 10^15).


## 解决方案


## 代码


