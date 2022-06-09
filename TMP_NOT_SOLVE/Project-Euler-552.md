---
title: Project Euler 552
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 552
## 题目
### Chinese leftovers II


Let <var>A_n</var> be the smallest positive integer satisfying  <var>A_n</var> mod <var>p_i</var> = <var>i</var>  for all 1 \le <var>i</var> \le <var>n</var>, where <var>p_i</var> is the
<var>i</var>-th prime.
<br />For example <var>A</var>_2 = 5, since this is the smallest positive solution of the system of equations 
<ul style="list-style-type:none;margin-left:2cm;"><li> <var>A</var>_2 mod 2 = 1 </li>
<li> <var>A</var>_2 mod 3 = 2</li></ul>
The system of equations for <var>A</var>_3 adds another constraint. That is, <var>A</var>_3 is the smallest positive solution of
<ul style="list-style-type:none;margin-left:2cm;"><li> <var>A</var>_3 mod 2 = 1 </li>
<li> <var>A</var>_3 mod 3 = 2</li>
<li> <var>A</var>_3 mod 5 = 3</li></ul>
and hence <var>A</var>_3 = 23. Similarly, one gets <var>A</var>_4 = 53 and <var>A</var>_5 = 1523.


Let S(<var>n</var>) be the sum of all primes up to <var>n</var> that divide at least one element in the sequence <var>A</var>.
<br />For example, S(50) = 69 = 5 + 23 + 41, since 5 divides <var>A</var>_2, 23 divides <var>A</var>_3 and 41 divides <var>A</var>_10 = 5765999453. No other prime number up to 50 divides an element in <var>A</var>.


Find S(300000).


# Project Euler 552
## 题目
### Chinese leftovers II

Let A_n be the smallest positive integer satisfying  A_n mod p_i = i  for all 1 \le i \le n, where p_i is the i-th prime.<br>For example A_2 = 5, since this is the smallest positive solution of the system of equations 
<ul>
<li>A_2 mod 2 = 1 </li>
<li>A_2 mod 3 = 2</li>
</ul>
The system of equations for A_3 adds another constraint. That is, A_3 is the smallest positive solution of
<ul>
<li>A_3 mod 2 = 1 </li>
<li>A_3 mod 3 = 2</li>
<li>A_3 mod 5 = 3</li>
</ul>
and hence A_3 = 23. Similarly, one gets A_4 = 53 and A_5 = 1523.
Let S(n) be the sum of all primes up to n that divide at least one element in the sequence A.<br>For example, S(50) = 69 = 5 + 23 + 41, since 5 divides A_2, 23 divides A_3 and 41 divides A_10 = 5765999453. No other prime number up to 50 divides an element in A.
Find S(300000).


## 解决方案


## 代码


