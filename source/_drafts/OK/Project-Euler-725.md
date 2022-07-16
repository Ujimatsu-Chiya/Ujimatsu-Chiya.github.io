---
title: Project Euler 725
tags:
  - Project Euler
  - 动态规划
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 725
## 题目
### Digit sum numbers



A number where one digit is the sum of the **other** digits is called a *digit sum number* or DS-number for short. For example, $352, 3003$ and $32812$ are DS-numbers.


We define $S(n)$ to be the sum of all DS-numbers of $n$ digits or less.


You are given $S(3) = 63270$ and $S(7) = 85499991450$.


Find $S(2020)$. Give your answer modulo $10^{16}$.




## 解决方案

令$N=2020.$一个数如果是DS数，那么它的数位和是最大数位的$2$倍。这不难想到使用动态规划来做。

令状态$c(i,s,d)(1\le i\le N,0\le s\le9,0\le d\le18)$表示当前有多少个$i$位**有前导0**数，其中数位之和为$s$，并且这$i$个数位中最大数位为$d.$

## 代码


