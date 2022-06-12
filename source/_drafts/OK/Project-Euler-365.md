---
title: Project Euler 365
tags:
  - Project Euler
  - 卢卡斯定理
  - 中国剩余定理
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 365
## 题目
### A huge binomial coefficient



The binomial coefficient $\displaystyle{\binom{10^{18}}{10^9}}$ is a number with more than 9 billion ($9\times 10^9$) digits.


Let $M(n,k,m)$ denote the binomial coefficient $\displaystyle{\binom{n}{k}}$ modulo $m$.


Calculate $\displaystyle{\sum M(10^{18},10^9,p\cdot q\cdot r)}$ for $1000\lt p\lt q\lt r\lt 5000$ and $p$,$q$,$r$ prime.








## 解决方案

令$pr$为所有满足$1000< p< 5000$的质数$p$的数组。

利用[卢卡斯定理](https://en.wikipedia.org/wiki/Lucas%27s_theorem)，可以预处理出所有$\displaystyle{\binom{10^{18}}{10^9}}\%p$的值。


## 代码


