---
title: Project Euler 794
category:
  - Project Euler
tags:
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 794
## 题目
### Seventeen Points


This problem uses half open interval notation where $[a,b)$ represents $a \le x < b$.

A real number, $x_1$, is chosen in the interval $[0,1)$.<br />
A second real number, $x_2$, is chosen such that each of $[0,\dfrac{1}{2})$ and $[\dfrac{1}{2},1)$ contains exactly one of $(x_1, x_2)$.<br />
Continue such that on the $n$-th step a real number, $x_n$, is chosen so that each of the intervals $[\dfrac{k-1}{n}, \dfrac{k}{n})$ for $k \in \{1, \dots, n\}$ contains exactly one of $(x_1, x_2, \dots, x_n)$.

Define $F(n)$ to be the minimal value of the sum $x_1 + x_2 + \dots + x_n$ of a tuple $(x_1, x_2, \dots, x_n)$ chosen by such a procedure. For example, $F(4) = 1.5$ obtained with $(x_1, x_2, x_3, x_4) = (0, 0.75, 0.5, 0.25)$.

Surprisingly, no more than $17$ points can be chosen by this procedure. 

Find $F(17)$ and give your answer rounded to $12$ decimal places.


## 解决方案


## 代码


