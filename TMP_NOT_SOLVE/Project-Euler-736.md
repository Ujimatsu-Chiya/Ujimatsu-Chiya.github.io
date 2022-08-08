---
title: Project Euler 736
category:
  - Project Euler
tags:
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 736
## 题目
### Paths to Equality


Define two functions on lattice points:
<center>$r(x,y) = (x+1,2y)$</center>
<center>$s(x,y) = (2x,y+1)$</center>
A <i>path to equality</i> of length $n$ for a pair $(a,b)$ is a sequence $\Big((a_1,b_1),(a_2,b_2),\ldots,(a_n,b_n)\Big)$, where:
<ul><li>$(a_1,b_1) = (a,b)$</li>
<li>$(a_k,b_k) = r(a_{k-1},b_{k-1})$ or $(a_k,b_k) = s(a_{k-1},b_{k-1})$ for $k > 1$</li>
<li>$a_k \ne b_k$ for $k < n$</li>
<li>$a_n = b_n$</li>
</ul>$a_n = b_n$ is called the <i>final value</i>.
For example,
<center>$(45,90)\xrightarrow{r} (46,180)\xrightarrow{s}(92,181)\xrightarrow{s}(184,182)\xrightarrow{s}(368,183)\xrightarrow{s}(736,184)\xrightarrow{r}$</center>
<center>$(737,368)\xrightarrow{s}(1474,369)\xrightarrow{r}(1475,738)\xrightarrow{r}(1476,1476)$</center>
This is a path to equality for $(45,90)$ and is of length 10 with final value 1476. There is no path to equality of $(45,90)$ with smaller length.
Find the unique path to equality for $(45,90)$ with smallest <b>odd</b> length. Enter the final value as your answer.



# Project Euler 736
## 题目
### Paths to Equality

Define two functions on lattice points:<br>$$r(x,y) = (x+1,2y)$$<br>$$s(x,y) = (2x,y+1)$$
A <i>path to equality</i> of length $n$ for a pair $(a,b)$ is a sequence $\Big((a_1,b_1),(a_2,b_2),\ldots,(a_n,b_n)\Big)$, where:
<ul>
<li>$(a_1,b_1) = (a,b)$</li>
<li>$(a_k,b_k) = r(a_{k-1},b_{k-1})$ or $(a_k,b_k) = s(a_{k-1},b_{k-1})$ for $k >1$</li>
<li>$a_k \ne b_k$ for $k<n$</li>
<li>$a_n = b_n$</li>
</ul>
$a_n = b_n$ is called the <i>final value</i>.
For example,<br>$$(45,90)\xrightarrow{r} (46,180)\xrightarrow{s}(92,181)\xrightarrow{s}(184,182)\xrightarrow{s}(368,183)\xrightarrow{s}(736,184)\xrightarrow{r}$$<br>$$(737,368)\xrightarrow{s}(1474,369)\xrightarrow{r}(1475,738)\xrightarrow{r}(1476,1476)$$
This is a path to equality for $(45,90)$ and is of length $10$ with final value $1476$. There is no path to equality of $(45,90)$ with smaller length.
Find the unique path to equality for $(45,90)$ with smallest **odd** length. Enter the final value as your answer.


## 解决方案


## 代码


