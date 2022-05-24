---
title: Project Euler 468
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 468
## 题目
### Smooth divisors of binomial coefficients

An integer is called **<var>B</var>-smooth** if none of its prime factors is greater than $B$.

Let $S_B(n)$ be the largest $B$-smooth divisor of $n$.<br />
Examples:<br />
$S_1(10)=1$<br />
$S_4(2100) = 12$<br />
$S_{17}(2496144) = 5712$
Define $\displaystyle F(n)=\sum_{B=1}^n \sum_{r=0}^n S_B(\binom n r)$. Here, $\displaystyle \binom n r$ denotes the binomial coefficient.<br />
Examples:<br />
$F(11) = 3132$<br />
$F(1111) \mod 1\,000\,000\,993 = 706036312$<br />
$F(111\,111) \mod 1\,000\,000\,993 = 22156169$

Find $F(11\,111\,111)  \mod 1\,000\,000\,993$.






# Project Euler 468
## 题目
### Smooth divisors of binomial coefficients

An integer is called **B-smooth** if none of its prime factors is greater than B.
Let S_B(n) be the largest B-smooth divisor of n.<br>Examples:
S_1(10) = 1<br>S_4(2100) = 12<br>S_17(2496144) = 5712
Define F(n) = \sum_1\leB\len \sum_0\ler\len S_B(C(n,r)). Here, C(n,r) denotes the binomial coefficient.<br>Examples:
F(11) = 3132<br>F(1&nbsp;111) mod 1&nbsp;000&nbsp;000&nbsp;993 = 706036312<br>F(111&nbsp;111) mod 1&nbsp;000&nbsp;000&nbsp;993 = 22156169
Find F(11&nbsp;111&nbsp;111) mod 1&nbsp;000&nbsp;000&nbsp;993.


## 解决方案


## 代码


