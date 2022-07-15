---
title: Project Euler 706
tags:
  - Project Euler
  - 动态规划
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 706
## 题目
### 3-Like Numbers



For a positive integer $n$, define $f(n)$ to be the number of non-empty substrings of $n$ that are divisible by $3$. For example, the string "$2573$" has $10$ non-empty substrings, three of which represent numbers that are divisible by $3$, namely $57, 573$ and $3$. So $f(2573) = 3$.


If $f(n)$ is divisible by $3$ then we say that $n$ is *$3$-like*.


Define $F(d)$ to be how many $d$ digit numbers are $3$-like. For example, $F(2) = 30$ and $F(6) = 290898$.


Find $F(10^5)$. Give your answer modulo $1\,000\,000\,007$.



## 解决方案

一个非常直接的动态规划题。

考虑到子串的个数，通常我们先将这个数$d=d_1d_2d_3\dots$看成一个字符串，然后令其前缀和数组为$s$，其中$s[0]=0,s[i]=s[i-1]+d_i$，那么一个数的子串和就可以通过数组$s$进行一次减法求得。

令$N=10^5$，假设已有状态$f(i,c_1,c_2,k,t)(1\le i\le N,0\le c_1,c_2,t<3)$为有多少个$i$位数满足以下条件：

- 令$c_0=(i+1-c_1-c_2)\%3$。这两个值其实也是状态之一，只不过可以被$i,c_1,c_2$表出。
- 目前数组$s$一共有$i+1$项，其中有$c_j$个项模$3$的值为$j(0\le j<3)$ ，注意$c_j$已经被$3$取模。
- 目前$s[i]$的值为$k$。
- 子串个数和$t$关于模$3$同余。

那么状态的转移只需要考虑在每个数后面添加一个数位$0\sim 9$，注意维护前缀和数组$s$新的一项。

本题转移过程考虑进行我为人人式。

不难知道初值

## 代码


