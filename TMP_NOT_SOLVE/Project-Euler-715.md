---
title: Project Euler 715
category:
  - Project Euler
tags:
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 715
## 题目
### Sextuplet Norms


Let $f(n)$ be the number of $6$-tuples $(x_1,x_2,x_3,x_4,x_5,x_6)$ such that:
<ul><li>All $x_i$ are integers with $0 \leq x_i < n$</li>
<li>$\gcd(x_1^2+x_2^2+x_3^2+x_4^2+x_5^2+x_6^2,\ n^2)=1$</li>
</ul>Let $\displaystyle G(n)=\displaystyle\sum_{k=1}^n \frac{f(k)}{k^2\varphi(k)}$<br />
where $\varphi(n)$ is Euler's totient function.

For example, $G(10)=3053$ and $G(10^5) \equiv 157612967 \pmod{1\,000\,000\,007}$.

Find $G(10^{12})\bmod 1\,000\,000\,007$.



# Project Euler 715
## 题目
### Sextuplet Norms

Let $f(n)$ be the number of $6$-tuples $(x_1,x_2,x_3,x_4,x_5,x_6)$ such that:
<ul>
<li>All $x_i$ are integers with $0 \leq x_i < n$</li>
<li>$\gcd(x_1^2+x_2^2+x_3^2+x_4^2+x_5^2+x_6^2,\ n^2)=1$</li>
</ul>
Let $\displaystyle G(n)=\displaystyle\sum_{k=1}^n \frac{f(k)}{k^2\varphi(k)}$<br>where $\varphi(n)$ is Euler’s totient function.
For example, $G(10)=3053$ and $G(10^5) \equiv 157612967 \pmod{1\ 000\ 000\ 007}$.
Find $G(10^{12})\bmod 1\ 000\ 000\ 007$.


## 解决方案


## 代码


