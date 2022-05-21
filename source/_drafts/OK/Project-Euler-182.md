---
title: Project Euler 182
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    

# Project Euler 182
## 题目
### RSA encryption

The RSA encryption is based on the following procedure:

Generate two distinct primes $p$ and $q$.Compute $n=pq$ and $\varphi=(p-1)(q-1)$.

Find an integer $e, 1<e<\varphi$, such that $\gcd(e,\varphi)=1$.

A message in this system is a number in the interval $[0,n-1]$.

A text to be encrypted is then somehow converted to messages (numbers in the interval $[0,n-1]$).

To encrypt the text,  for each message, $m, c=m^e \mod n$ is calculated.

To decrypt the text, the following procedure is needed: calculate $d$ such that $ed=1 \mod \varphi$, then for each encrypted message, $c$, calculate $m=c^d \mod n$.

There exist values of $e$ and $m$  such that $m^e \mod n=m$.

We call messages $m$ for which $m^e \mod n=m$ unconcealed messages.

An issue when choosing e is that there should not be too many unconcealed messages.

For instance, let $p=19$ and $q=37$.

Then $n=19*37=703$ and $\varphi=18*36=648$.

If we choose $e=181$, then, although $\gcd(181,648)=1$ it turns out that all possible messages $m (0\le m\le n-1)$ are unconcealed when calculating $m^e \mod n$.

For any valid choice of e there exist some unconcealed messages.It’s important that the number of unconcealed messages is at a minimum.

Choose $p=1009$ and $q=3643$.

Find the sum of all values of $e$, $1<e<\varphi(1009,3643)$ and $\gcd(e,\varphi)=1$, so that the number of unconcealed messages for this value of $e$ is at a minimum.


## 解决方案

不难发现，$m^e\equiv m(\mod n)\Rightarrow m^e\equiv m(\mod p)\wedge m^e \equiv m(\mod q)$

容易发现，当$m=0$时，为一个解。其余$m$满足$p \mid m$或者$q\mid m$都不是解。

对于其余情况，不失一般性，仅解$m^e\equiv m(\mod p)$，那么有$m^{e-1}\equiv 1(\mod p)$。

原问题转化成关于$m$的方程$m^{e-1}\equiv 1(\mod p)$有多少个解集。

设$g$为群$\mathbb{Z}_p^*$中的一个原根（原根：对于群元素$g$，假设$x$是满足$g^x\equiv1(\mod p)$的最小正整数，如果$x=p-1$，那么$g$为群$\mathbb{Z}_p^*$）。根据原根的定义，对于任意整数$i\in\{0,1,\dots,p-2\}$，$g^i$都可以和群元素$a$一一对应。



## 代码

设$\lambda_p(a)$表示群元素$a$在模质数$p$乘法群$\mathbb{Z}_p^*$中的阶，即$\lambda_p(a)=x$表示最小的正整数$x$使得$a^x\equiv1(\mod p)$。根据费马小定理，有$\lambda_p(a)\mid\varphi(p)$。


对于群$\mathbb{Z}_p^*$中的任意一个元素$\{1,2,\dots,p-1\}$，


因此，如果一个整数$k$满足$a^k\equiv1(\mod p)$，那么$\lambda_p(a)\mid k$。