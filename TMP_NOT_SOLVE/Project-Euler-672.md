---
title: Project Euler 672
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 672
## 题目
### One more one

Consider the following process that can be applied recursively to any positive integer $n$:
<ul><li>if $n = 1$ do nothing and the process stops,</li>
<li>if $n$ is divisible by 7 divide it by 7,</li>
<li>otherwise add 1.</li>
</ul>Define $g(n)$ to be the number of 1's that must be added before the process ends. For example:
<center>$125\xrightarrow{\scriptsize{+1}} 126\xrightarrow{\scriptsize{\div 7}} 18\xrightarrow{\scriptsize{+1}} 19\xrightarrow{\scriptsize{+1}} 20\xrightarrow{\scriptsize{+1}} 21\xrightarrow{\scriptsize{\div 7}} 3\xrightarrow{\scriptsize{+1}} 4\xrightarrow{\scriptsize{+1}} 5\xrightarrow{\scriptsize{+1}} 6\xrightarrow{\scriptsize{+1}} 7\xrightarrow{\scriptsize{\div 7}} 1$.</center>
Eight 1's are added so $g(125) = 8$. Similarly $g(1000) = 9$ and $g(10000) = 21$.
Define $S(N) = \sum_{n=1}^{N} g(n)$ and $H(K) = S\left(\frac{7^K-1}{11}\right)$. You are given $H(10) = 690409338$.
Find $H(10^9)$ modulo $1\,117\,117\,717$.


# Project Euler 672
## 题目
### One more one

Consider the following process that can be applied recursively to any positive integer $n$:
<ul>
<li>if $n = 1$ do nothing and the process stops,</li>
<li>if $n$ is divisible by $7$ divide it by $7$,</li>
<li>otherwise add $1$.</li>
</ul>
Define $g(n)$ to be the number of $1$’s that must be added before the process ends. For example:
$$125\xrightarrow{\scriptsize{+1}} 126\xrightarrow{\scriptsize{\div 7}} 18\xrightarrow{\scriptsize{+1}} 19\xrightarrow{\scriptsize{+1}} 20\xrightarrow{\scriptsize{+1}} 21\xrightarrow{\scriptsize{\div 7}} 3\xrightarrow{\scriptsize{+1}} 4\xrightarrow{\scriptsize{+1}} 5\xrightarrow{\scriptsize{+1}} 6\xrightarrow{\scriptsize{+1}} 7\xrightarrow{\scriptsize{\div 7}} 1$$
Eight $1$’s are added so $g(125) = 8$. Similarly $g(1000) = 9$ and $g(10000) = 21$.
Define $S(N) = \sum_{n=1}^{N} g(n)$ and $H(K) = S\left(\frac{7^K-1}{11}\right)$. You are given $H(10) = 690409338$.
Find $H(10^9)$ modulo $1,117,117,717$.


## 解决方案


## 代码

