---
title: Project Euler 462
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 462
## 题目
### Permutation of 3-smooth numbers


A <b>3-smooth number</b> is an integer which has no prime factor larger than 3. For an integer <var>N</var>, we define S(<var>N</var>) as the set of 3-smooth numbers less than or equal to <var>N</var> . For example, S(20) = { 1, 2, 3, 4, 6, 8, 9, 12, 16, 18 }.


We define F(<var>N</var>) as the number of permutations of S(<var>N</var>) in which each element comes after all of its proper divisors.


This is one of the possible permutations for <var>N</var> = 20.<br />
- 1, 2, 4, 3, 9, 8, 16, 6, 18, 12.<br />
This is not a valid permutation because 12 comes before its divisor 6.<br />
- 1, 2, 4, 3, 9, 8, <b>12</b>, 16, <b>6</b>, 18.


We can verify that F(6) = 5, F(8) = 9, F(20) = 450 and F(1000) ≈ 8.8521816557e21.<br />
Find F(10^18). Give as your answer its scientific notation rounded to ten digits after the decimal point.<br />
When giving your answer, use a lowercase e to separate mantissa and exponent. E.g. if the answer is 112,233,445,566,778,899 then the answer format would be 1.1223344557e17.



# Project Euler 462
## 题目
### Permutation of 3-smooth numbers

A **3-smooth number** is an integer which has no prime factor larger than 3. For an integer N, we define S(N) as the set of 3-smooth numbers less than or equal to N . For example, S(20) = { 1, 2, 3, 4, 6, 8, 9, 12, 16, 18 }.
We define F(N) as the number of permutations of S(N) in which each element comes after all of its proper divisors.
This is one of the possible permutations for N = 20.<br>1, 2, 4, 3, 9, 8, 16, 6, 18, 12.<br>This is not a valid permutation because 12 comes before its divisor 6.<br>1, 2, 4, 3, 9, 8, **12**, 16, **6**, 18.
We can verify that F(6) = 5, F(8) = 9, F(20) = 450 and F(1000) ≈ 8.8521816557e21.<br>Find F(10^18). Give as your answer its scientific notation rounded to ten digits after the decimal point.<br>When giving your answer, use a lowercase e to separate mantissa and exponent. E.g. if the answer is 112,233,445,566,778,899 then the answer format would be 1.1223344557e17.


## 解决方案


## 代码


