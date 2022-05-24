---
title: Project Euler 467
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 467
## 题目
### Superinteger

An integer <var>s</var> is called a <em>superinteger</em> of another integer <var>n</var> if the digits of <var>n</var> form a <dfn title="A subsequence is a sequence that can be derived from another sequence by deleting some elements without changing the order of the remaining elements.">subsequence</dfn> of the digits of <var>s</var>.<br />
For example, 2718281828 is a superinteger of 18828, while 314159 is not a superinteger of 151.


Let <var>p</var>(<var>n</var>) be the <var>n</var>th prime number, and let <var>c</var>(<var>n</var>) be the <var>n</var>th composite number. For example, <var>p</var>(1) = 2, <var>p</var>(10) = 29, <var>c</var>(1) = 4 and <var>c</var>(10) = 18.<br />
{<var>p</var>(<var>i</var>) : i \ge 1} = {2, 3, 5, 7, 11, 13, 17, 19, 23, 29, \dots}<br />
{<var>c</var>(<var>i</var>) : i \ge 1} = {4, 6, 8, 9, 10, 12, 14, 15, 16, 18, \dots}

Let P^D the sequence of the **digital roots** of {<var>p</var>(<var>i</var>)} (C^D is defined similarly for {<var>c</var>(<var>i</var>)}):<br />
P^D = {2, 3, 5, 7, 2, 4, 8, 1, 5, 2, \dots}<br />
C^D = {4, 6, 8, 9, 1, 3, 5, 6, 7, 9, \dots}

Let P_<var>n</var> be the integer formed by concatenating the first <var>n</var> elements of P^D (C_<var>n</var> is defined similarly for C^D).<br />
P_10 = 2357248152<br />
C_10 = 4689135679

Let <var>f</var>(<var>n</var>) be the smallest positive integer that is a common superinteger of P_<var>n</var> and C_<var>n</var>. <br />For example, <var>f</var>(10) = 2357246891352679, and <var>f</var>(100) mod 1 000 000 007 = 771661825.

Find <var>f</var>(10 000) mod 1 000 000 007.


# Project Euler 467
## 题目
### Superinteger

An integer s is called a <em>superinteger</em> of another integer n if the digits of n form a <dfn title="A subsequence is a sequence that can be derived from another sequence by deleting some elements without changing the order of the remaining elements.">subsequence</dfn> of the digits of s.<br>For example, 2718281828 is a superinteger of 18828, while 314159 is not a superinteger of 151.
Let p(n) be the nth prime number, and let c(n) be the nth composite number. For example, p(1) = 2, p(10) = 29, c(1) = 4 and c(10) = 18.<br>{p(i) : i \ge 1} = {2, 3, 5, 7, 11, 13, 17, 19, 23, 29, \dots}<br>{c(i) : i \ge 1} = {4, 6, 8, 9, 10, 12, 14, 15, 16, 18, \dots}
Let P^D the sequence of the **digital roots** of {p(i)} (C^D is defined similarly for {c(i)}):<br>P^D = {2, 3, 5, 7, 2, 4, 8, 1, 5, 2, \dots}<br>C^D = {4, 6, 8, 9, 1, 3, 5, 6, 7, 9, \dots}
Let P_n be the integer formed by concatenating the first n elements of P^D (C_n is defined similarly for C^D).<br>P_10 = 2357248152<br>C_10 = 4689135679
Let f(n) be the smallest positive integer that is a common superinteger of P_n and C_n.<br>For example, f(10) = 2357246891352679, and f(100) mod 1&nbsp;000&nbsp;000&nbsp;007 = 771661825.
Find f(10&nbsp;000) mod 1&nbsp;000&nbsp;000&nbsp;007.


## 解决方案


## 代码


