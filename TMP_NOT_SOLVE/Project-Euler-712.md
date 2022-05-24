---
title: Project Euler 712
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 712
## 题目
### Exponent Difference


For any integer $n>0$ and prime number $p,$ define $\nu_p(n)$ as the greatest integer $r$ such that $p^r$ divides $n$. 


Define $$D(n, m)  = \sum_{p \text{ prime}} \left| \nu_p(n) - \nu_p(m)\right|.$$ For example, $D(14,24) = 4$.


Furthermore, define $$S(N) = \sum_{1 \le n, m \le N} D(n, m).$$ You are given $S(10) = 210$ and $S(10^2) = 37018$.


Find $S(10^{12})$. Give your answer modulo $1\,000\,000\,007$.



# Project Euler 712
## 题目
### Exponent Difference

For any integer $n>0$ and prime number $p$, define $\nu_p(n)$ as the greatest integer $r$ such that $p^r$ divides $n$. 
Define<br>$$D(n, m)  = \sum_{p \text{ prime}} \left| \nu_p(n) - \nu_p(m)\right|.$$<br>For example, $D(14,24) = 4$.
Furthermore, define<br>$$S(N) = \sum_{1 \le n, m \le N} D(n, m).$$<br>You are given $S(10) = 210$ and $S(10^2) = 37018$.
Find $S(10^{12})$. Give your answer modulo $1\ 000\ 000\ 007$.


## 解决方案


## 代码

