---
title: Project Euler 445
category:
  - Project Euler
tags:
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 445
## 题目
### Retractions A



For every integer $n>1$, the family of functions $f_{n,a,b}$ is defined 
by  <br />
$f_{n,a,b}(x)\equiv a x + b \mod n\,\,\, $ for $a,b,x$ integer and  $0< a <n, 0 \le b < n,0 \le x < n$. 

We will call $f_{n,a,b}$ a <i>retraction</i> if $\,\,\, f_{n,a,b}(f_{n,a,b}(x)) \equiv f_{n,a,b}(x) \mod n \,\,\,$ for every $0 \le x < n$.<br />
Let $R(n)$ be the number of retractions for $n$.


You are given that<br />
$\displaystyle \sum_{k=1}^{99\,999} R(\binom {100\,000} k)  \equiv 628701600 \mod 1\,000\,000\,007$.
 
Find $\displaystyle \sum_{k=1}^{9\,999\,999} R(\binom {10\,000\,000} k)$.<br />
Give your answer modulo $1\,000\,000\,007$.





# Project Euler 445
## 题目
### Retractions A

For every integer n>1, the family of functions f_n,a,b  is defined by f_n,a,b(x)≡ax+b mod n for a,b,x integer and  0<a<n, 0\leb<n, 0\lex<n.<br>We will call f_n,a,b a retraction if f_n,a,b(f_n,a,b(x))≡f_n,a,b(x) mod n for every 0\lex<n.<br>Let R(n) be the number of retractions for n.
You are given that<br>\sum R(c) for c=C(100 000,k), and 1 \le k \le99 999 ≡628701600 (mod 1 000 000 007).<br>(C(n,k) is the binomial coefficient).
Find \sum R(c) for c=C(10 000 000,k), and 1 \lek\le 9 999 999.<br>Give your answer modulo 1 000 000 007.


## 解决方案


## 代码


