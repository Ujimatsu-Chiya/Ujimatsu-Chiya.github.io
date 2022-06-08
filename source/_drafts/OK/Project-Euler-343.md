---
title: Project Euler 343
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    



# Project Euler 343
## 题目
### Fractional Sequences

For any positive integer $k$, a finite sequence $a_i$ of fractions $\dfrac{x_i}{y_i}$ is defined by:

$a_1 = \dfrac{1}{k}$ and $a_i = \dfrac{x_{i-1}+1}{y_{i-1}-1}$ reduced to lowest terms for $i>1$.

When $a_i$ reaches some integer $n$, the sequence stops. (That is, when $y_i=1$.)

Define $f(k) = n$.

For example, for $k = 20$:

$\dfrac{1}{20} \rightarrow \dfrac{2}{19} \rightarrow \dfrac{3}{18} = \dfrac{1}{6} \rightarrow \dfrac{2}{5} \rightarrow \dfrac{3}{4} \rightarrow \dfrac{4}{3} \rightarrow \dfrac{5}{2} \rightarrow \dfrac{6}{1} = 6$

So $f(20) = 6$.

Also $f(1) = 1, f(2) = 2, f(3) = 1$ and $\sum f(k^3) = 118937$ for $1 \le k \le 100$.

Find $\sum f(k^3)$ for $1 \le k \le 2\times10^6$.


## 解决方案


## 代码


