---
title: Project Euler 181
tags:
  - Project Euler
  - 动态规划
mathjax: true
---
<escape><!-- more --></escape>
    

# Project Euler 181
## 题目
### Investigating in how many ways objects of two different colours can be grouped

Having three black objects B and one white object W they can be grouped in 7 ways like this:

||||||||
|-|-|-|-|-|-|-|
|(BBBW)|(B,BBW)|(B,B,BW)|(B,B,B,W)|(B,BB,W)|(BBB,W)|(BB,BW)|

In how many ways can sixty black objects B and forty white objects W be  thus grouped?


## 解决方案

令$N=60,M=40$。不难发现，一个**非空**的内部组合一共有$O=(N+1)(M+1)-1$种不同情况。

为了使得计数不重不漏，我们规定了一种内部组合的”顺序“，其中第$k(k\le O)$种内部组合包含了$x[k]$个黑色物体，$y[k]$个白色物体，而$p[i][j]$表示$i$个黑色物体和$j$个白色物体的内部组合序号。

如果第$k$种内部组合已经出现了，那么以后就只能使用$k,k+1,\dots,O$的内部组合，不能再使用以前的组合。

那么，使用动态规划的方法进行计数。令$f(i,j,k)(0\le i\le N,0\le j\le M,1\le k\le O)$表示已经使用了$i$个黑色物体和$j$个白色物体，内部组合使用序号已经到达了$k$的情况。


$$
\mu(n)=
\left \{\begin{aligned}
  &1 & & \mathrm{if\quad} n=1 \\
  &0 & & \mathrm{else if\quad} \exist m\in[1,k],e_m>1 \\
  &(-1)^k & & \mathrm{else}
\end{aligned}\right.
$$

## 代码


