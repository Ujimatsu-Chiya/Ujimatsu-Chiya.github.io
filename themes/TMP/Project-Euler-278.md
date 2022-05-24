---
title: Project Euler 278
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 278
## 题目
### Linear Combinations of Semiprimes


Given the values of integers $1 < a_1 < a_2 < \dots < a_n$, consider the linear combination<br />
$q_1 a_1+q_2 a_2 + \dots + q_n a_n=b$, using only integer values $q_k \ge 0$. 


Note that for a given set of $a_k$, it may be that not all values of $b$ are possible.<br />
For instance, if $a_1=5$ and $a_2=7$, there are no $q_1 \ge 0$ and $q_2 \ge 0$ such that $b$ could be<br /> 
$1, 2, 3, 4, 6, 8, 9, 11, 13, 16, 18$ or $23$.
<br />
In fact, $23$ is the largest impossible value of $b$ for $a_1=5$ and $a_2=7$.<br /> We therefore call $f(5, 7) = 23$.<br /> Similarly, it can be shown that $f(6, 10, 15)=29$ and $f(14, 22, 77) = 195$.


Find $\displaystyle \sum f( p\, q,p \, r, q \, r)$, where $p$, $q$ and $r$ are prime numbers and $p < q < r < 5000$.





# Project Euler 278
## 题目
### Linear Combinations of Semiprimes

Given the values of integers 1 < a_1 < a_2 <\dots < a_n, consider the linear combination q_1a_1 + q_2a_2 + \dots + q_na_n = b, using only integer values q_k \ge 0. 
Note that for a given set of a_k, it may be that not all values of b are possible.<br>For instance, if a_1 = 5 and a_2 = 7, there are no q_1 \ge 0 and q_2 \ge 0 such that b could be 1, 2, 3, 4, 6, 8, 9, 11, 13, 16, 18 or 23.<br>In fact, 23 is the largest impossible value of b for a_1 = 5 and a_2 = 7.<br>We therefore call f(5, 7) = 23.<br>Similarly, it can be shown that f(6, 10, 15)=29 and f(14, 22, 77) = 195.
Find \sum f(p*q,p*r,q*r), where p, q and r are prime numbers and p < q < r < 5000.


## 解决方案


## 代码


