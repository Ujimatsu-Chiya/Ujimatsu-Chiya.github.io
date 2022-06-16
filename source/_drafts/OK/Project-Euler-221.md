---
title: Project Euler 221
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    

# Project Euler 221
## 题目
### Alexandrian Integers

We shall call a positive integer $A$ an “Alexandrian integer”, if there exist integers $p, q, r$ such that:

$$A=p·q·r \text{ and } \frac{1}{A}=\frac{1}{p}+\frac{1}{q}+\frac{1}{r}$$

For example, $630$ is an Alexandrian integer ($p = 5, q = -7, r = -18$). 

In fact, $630$ is the $6^{\text{th}}$ Alexandrian integer,  the first $6$ Alexandrian integers being: $6, 42, 120, 156, 420$ and $630$.

Find the $150000^{\text{th}}$ Alexandrian integer.


## 解决方案

可以发现，$p,q,r$中必定有其中一个数是正数，其余两个数是负数，假设$p$是正数，$q,r$是负数。

因此问题等价于如下形式：

寻找$A=pqr$，其中$p,q,r>0$，使得$\dfrac{1}{A}=\dfrac{1}{p}-\dfrac{1}{q}-\dfrac{1}{r}$

消去$A$，不难得到

$$qr-pr-qp=1$$

两边都添加一个$p^2$，那么可以写成

$$(p-q)(p-r)=p^2+1$$

那么，先枚举$p$，再枚举$p^2+1$的因子$d$，那么可以得到$p-q=d,p-r=\dfrac{p^2+1}{d}$，最终得到题目中要求的一个数：

$$A=p(p+d)(p+\dfrac{p^2+1}{d})$$

## 代码


