---
title: Project Euler 425
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 425
## 题目
### Prime connection


Two positive numbers A and B are said to be <i>connected</i> (denoted by "A ↔ B") if one of these conditions holds:<br />
(1) A and B have the same length and differ in exactly one digit; for example, 123 ↔ 173.<br />
(2) Adding one digit to the left of A (or B) makes B (or A); for example, 23 ↔ 223 and 123 ↔ 23.


We call a prime P a <i>2's relative</i> if there exists a chain of connected primes between 2 and P and no prime in the chain exceeds P.


For example, 127 is a 2's relative. One of the possible chains is shown below:<br />
2 ↔ 3 ↔ 13 ↔ 113 ↔ 103 ↔ 107 ↔ 127<br />
However, 11 and 103 are not 2's relatives.


Let F(N) be the sum of the primes \le N which are not 2's relatives.<br />
We can verify that F(10^3) = 431 and F(10^4) = 78728.


Find F(10^7).



# Project Euler 425
## 题目
### Prime connection

Two positive numbers A and B are said to be <em>connected</em> (denoted by “A ↔ B”) if one of these conditions holds:<br>(1) A and B have the same length and differ in exactly one digit; for example, 123 ↔ 173.<br>(2) Adding one digit to the left of A (or B) makes B (or A); for example, 23 ↔ 223 and 123 ↔ 23.
We call a prime P a <em>2’s relative</em> if there exists a chain of connected primes between 2 and P and no prime in the chain exceeds P.
For example, 127 is a 2’s relative. One of the possible chains is shown below:<br>2 ↔ 3 ↔ 13 ↔ 113 ↔ 103 ↔ 107 ↔ 127<br>However, 11 and 103 are not 2’s relatives.
Let F(N) be the sum of the primes \le N which are not 2’s relatives.<br>We can verify that F(10^3) = 431 and F(10^4) = 78728.
Find F(10^7).


## 解决方案


## 代码


