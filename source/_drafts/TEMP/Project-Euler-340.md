---
title: Project Euler 340
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 340
## 题目
### Crazy Function


For fixed integers a, b, c, define the <i>crazy function</i> F(<var>n</var>) as follows:<br />
F(<var>n</var>) = <var>n</var> - c for all <var>n</var> > b <br />
F(<var>n</var>) = F(a + F(a + F(a + F(a + <var>n</var>)))) for all <var>n</var> \le b.

Also, define $S(a, b, c) = \sum \limits_{n = 0}^{b} {F(n)}$.

For example, if a = 50, b = 2000 and c = 40, then F(0) = 3240 and F(2000) = 2040.<br />
Also, S(50, 2000, 40) = 5204240.


Find the last 9 digits of S(21^7, 7^21, 12^7).








# Project Euler 340
## 题目
### Crazy Function

For fixed integers a, b, c, define the <i>crazy function</i> F(n) as follows:<br>F(n) = n - c for all n > b<br>F(n) = F(a + F(a + F(a + F(a + n)))) for all n \le b
Also, define S(a, b, c) = $\sum_{n=0}^{b}F(n)$.
For example, if a = 50, b = 2000 and c = 40, then F(0) = 3240 and F(2000) = 2040.<br>Also, S(50, 2000, 40) = 5204240.
Find the last 9 digits of S(21^7, 7^21, 12^7).


## 解决方案


## 代码


