---
title: Project Euler 561
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 561
## 题目
### Divisor Pairs



Let $S(n)$ be the number of pairs $(a,b)$ of distinct divisors of $n$ such that $a$ divides $b$.

For $n=6$ we get the following pairs: $(1,2), (1,3), (1,6),( 2,6)$ and $(3,6)$. So $S(6)=5$.

Let $p_m\#$ be the product of the first $m$ prime numbers,  so $p_2\# = 2*3 = 6$.

Let $E(m, n)$ be the highest integer $k$ such that $2^k$ divides $S((p_m\#)^n)$.

$E(2,1) = 0$ since $2^0$ is the highest power of $2$ that divides $S(6)=5$.

Let $Q(n)=\sum_{i=1}^{n} E(904961, i)$

$Q(8)=2714886$.

Evaluate $Q(10^{12})$. 



## 解决方案

令$n$的分解质因数为$n=\prod_{i=1}^m p_i^{e_i}$。那么，$S(n)$的求解就化为以下问题：

有多少对$m$维向量$(\vec{a},\vec{b})$，其中$\vec{a}=(a_1,a_2,\dots,a_m),\vec{b}=(b_1,b_2,\dots,b_m)$，满足$\forall i\in[1,m],0\le a_i\le b_i\le e_i$，并且$\vec{a}\neq \vec{b}$？

不难计算出$S(n)=\prod_{i=1}^m \dfrac{(e_i+1)(e_i+2)}{2}-\prod_{i=1}^m (e_i+1)$

计算$S((p_m\#)^n)$时，可以发现$e_1=e_2=\dots=e_m=n$。

因此，

$$S((p_m\#)^n)=(\dfrac{(n+1)(n+2)}{2})^m-(n+1)^m$$

## 代码


