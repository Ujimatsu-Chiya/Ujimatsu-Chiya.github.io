---
title: Project Euler 423
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 423
## 题目
### Consecutive die throws

Let <var>n</var> be a positive integer.<br />
A 6-sided die is thrown <var>n</var> times. Let <var>c</var> be the number of pairs of consecutive throws that give the same value.

For example, if <var>n</var> = 7 and the values of the die throws are (1,1,5,6,6,6,3), then the following pairs of consecutive throws give the same value:<br />
(<u>1,1</u>,5,6,6,6,3)<br />
(1,1,5,<u>6,6</u>,6,3)<br />
(1,1,5,6,<u>6,6</u>,3)<br />
Therefore, <var>c</var> = 3 for (1,1,5,6,6,6,3).

Define C(<var>n</var>) as the number of outcomes of throwing a 6-sided die <var>n</var> times such that <var>c</var> does not exceed π(<var>n</var>).^1<br />
For example, C(3) = 216, C(4) = 1290, C(11) = 361912500 and C(24) = 4727547363281250000.

Define S(<var>L</var>) as <span style="font-size:larger;"><span style="font-size:larger;">\sum</span></span> C(<var>n</var>) for 1 \le <var>n</var> \le <var>L</var>.<br />
For example, S(50) mod 1 000 000 007 = 832833871.

Find S(50 000 000) mod 1 000 000 007.

 <span style="font-size:smaller;">^1 π denotes the <b>prime-counting function</b>, i.e. π(<var>n</var>) is the number of primes \le <var>n</var>.</span>


# Project Euler 423
## 题目
### Consecutive die throws

Let n be a positive integer.<br>A 6-sided die is thrown n times. Let c be the number of pairs of consecutive throws that give the same value.
For example, if n = 7 and the values of the die throws are (1,1,5,6,6,6,3), then the following pairs of consecutive throws give the same value:<br>(<u>1,1</u>,5,6,6,6,3)<br>(1,1,5,<u>6,6</u>,6,3)<br>(1,1,5,6,<u>6,6</u>,3)<br>Therefore, c = 3 for (1,1,5,6,6,6,3).
Define C(n) as the number of outcomes of throwing a 6-sided die n times such that c does not exceed π(n).^1<br>For example, C(3) = 216, C(4) = 1290, C(11) = 361912500 and C(24) = 4727547363281250000.
Define S(L) as \sum C(n) for 1 \le n \le L.<br>For example, S(50) mod 1&nbsp;000&nbsp;000&nbsp;007 = 832833871.
Find S(50&nbsp;000&nbsp;000) mod 1&nbsp;000&nbsp;000&nbsp;007.
^1 π denotes the **prime-counting function**, i.e. π(n) is the number of primes \le n.


## 解决方案


## 代码


