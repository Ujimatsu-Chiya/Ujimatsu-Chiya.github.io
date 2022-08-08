---
title: Project Euler 447
category:
  - Project Euler
tags:
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 447
## 题目
### Retractions C



For every integer $n>1$, the family of functions $f_{n,a,b}$ is defined 
by  <br />
$f_{n,a,b}(x)\equiv a x + b \mod n\,\,\, $ for $a,b,x$ integer and  $0< a <n, 0 \le b < n,0 \le x < n$. 

We will call $f_{n,a,b}$ a <i>retraction</i> if $\,\,\, f_{n,a,b}(f_{n,a,b}(x)) \equiv f_{n,a,b}(x) \mod n \,\,\,$ for every $0 \le x < n$.<br />
Let $R(n)$ be the number of retractions for $n$.


$\displaystyle F(N)=\sum_{n=2}^N R(n)$. <br /> 
$F(10^7)\equiv 638042271 \mod 1\,000\,000\,007$.<br />

Find $F(10^{14})$.<br />
Give your answer modulo $1\,000\,000\,007$.





# Project Euler 447
## 题目
### Retractions C

For every integer n>1, the family of functions f_n,a,b  is defined by f_n,a,b(x)≡ax+b mod n for a,b,x integer and  0<a<n, 0\leb<n, 0\lex<n.<br>We will call f_n,a,b a retraction if f_n,a,b(f_n,a,b(x))≡f_n,a,b(x) mod n for every 0\lex<n.<br>Let R(n) be the number of retractions for n.
F(N)=\sumR(n) for 2\len\leN.<br>F(10^7)≡638042271 (mod 1 000 000 007).
Find F(10^14) (mod 1 000 000 007).


## 解决方案


## 代码


