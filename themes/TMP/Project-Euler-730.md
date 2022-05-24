---
title: Project Euler 730
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 730
## 题目
### Shifted Pythagorean Triples


For a non-negative integer $k$, the triple $(p,q,r)$ of positive integers is called a <dfn>$k$-shifted Pythagorean triple</dfn> if $$p^2 + q^2 + k = r^2$$


$(p, q, r)$ is said to be primitive if $\gcd(p, q, r)=1$.


Let $P_k(n)$ be the number of primitive k-shifted Pythagorean triples such that $1 \le p \le q \le r$ and $p + q + r \le n$. <br /> For example, $P_0(10^4) = 703$ and $P_{20}(10^4) = 1979$. 


Define 
$$\displaystyle S(m,n)=\sum_{k=0}^{m}P_k(n)$$
You are given that $S(10,10^4) = 10956$. 


Find $S(10^2,10^8)$



# Project Euler 730
## 题目
### Shifted Pythagorean Triples

For a non-negative integer $k$, the triple $(p,q,r)$ of positive integers is called a <i>$k$-shifted Pythagorean triple</i> if $$p^2 + q^2 + k = r^2$$
$(p, q, r)$ is said to be primitive if $\gcd(p, q, r)=1$.
Let $P_k(n)$ be the number of primitive k-shifted Pythagorean triples such that $1 \le p \le q \le r$ and $p + q + r \le n$.<br>For example, $P_0(10^4) = 703$ and $P_{20}(10^4) = 1979$. 
Define<br>$$\displaystyle S(m,n)=\sum_{k=0}^{m}P_k(n)$$<br>You are given that $S(10,10^4) = 10956$. 
Find $S(10^2,10^8)$.


## 解决方案


## 代码


