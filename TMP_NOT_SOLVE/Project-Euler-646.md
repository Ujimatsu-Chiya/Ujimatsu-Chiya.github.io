---
title: Project Euler 646
category:
  - Project Euler
tags:
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 646
## 题目
### Bounded Divisors



Let $n$ be a natural number and  $p_1^{\alpha_1}\cdot p_2^{\alpha_2}\dotsp_k^{\alpha_k}$ its prime factorisation.<br />
Define the <b>Liouville function</b> $\lambda(n)$ as $\lambda(n) = (-1)^{\sum\limits_{i=1}^{k}\alpha_i}$.<br />
(i.e. $-1$ if the sum of the exponents $\alpha_i$ is odd and $1$ if the sum of the exponents is even. )<br />
Let $S(n,L,H)$  be the sum $\lambda(d) \cdot d$ over all divisors $d$ of $n$ for which $L \leq d \leq H$.


You are given:<br />
$\bullet\, S(10! , 100, 1000) = 1457$<br />
$\bullet\, S(15!,  10^3, 10^5) = -107974$<br />
$\bullet\, S(30!,10^8, 10^{12}) = 9766732243224$.<br />

Find $S(70!,10^{20}, 10^{60})$ and give your answer modulo $1\,000\,000\,007$.




# Project Euler 646
## 题目
### Bounded Divisors

Let $n$ be a natural number and $p_1^{\alpha_1}\cdot p_2^{\alpha_2}\cdots p_k^{\alpha_k}$ its prime factorisation.
Define the **Liouville function** $\lambda(n)$ as $\lambda(n)=(-1)^{\sum_{i=1}^k\alpha_i}$.<br>(i.e. $-1$ if the sum of the exponents $\alpha_i$ is odd and $1$ if the sum of the exponents is even. )<br>Let $S(n,L,H)$ be the sum $\lambda(d)\cdot d$ over all divisors $d$ of $n$ for which $L\le d\le H$.
You are given:<br>$S(10!,100,1000)=1457$<br>$S(15!,10^3,10^5)=-107974$<br>$S(30!,10^8,10^{12})=9766732243224$
Find $S(70!,10^{20},10^{60})$ and give your answer modulo $1\ 000\ 000\ 007$.


## 解决方案


## 代码


