---
title: Project Euler 182
tags:
  - Project Euler
mathjax: true
date: 2022-05-24 11:02:33
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

Then $n=19\times37=703$ and $\varphi=18\times36=648$.

If we choose $e=181$, then, although $\gcd(181,648)=1$ it turns out that all possible messages $m (0\le m\le n-1)$ are unconcealed when calculating $m^e \mod n$.

For any valid choice of e there exist some unconcealed messages.It’s important that the number of unconcealed messages is at a minimum.

Choose $p=1009$ and $q=3643$.

Find the sum of all values of $e$, $1<e<\varphi(1009,3643)$ and $\gcd(e,\varphi)=1$, so that the number of unconcealed messages for this value of $e$ is at a minimum.

## 解决方案

不难发现，$m^e\equiv m(\mod n)\Rightarrow m^e\equiv m(\mod p)\wedge m^e \equiv m(\mod q)$

容易发现，当$m=0$时，为一个解。其余$m$满足$p \mid m$或者$q\mid m$都不是解。

对于其余情况，不失一般性，仅解$m^e\equiv m(\mod p)$，那么有$m^{e-1}\equiv 1(\mod p)$。

原问题转化成关于$m$的方程$m^{e-1}\equiv 1(\mod p)$有多少个解。令$r=e-1$。

设$g$为群$\mathbb{Z}_p^{\star}$中的一个原根（原根：对于群元素$g$，假设$x$是满足$g^x\equiv1(\mod p)$的最小正整数，如果$x=p-1$，那么$g$为群$\mathbb{Z}_p^{\star}$）。根据原根的定义，对于任意整数$i\in\{0,1,\dots,p-2\}$，$g^i$都可以和群元素$a$一一对应。

令$m=g^i$，那么问题转化成$g^{ri}\equiv1(\mod p)$有多少个$i$是满足此式的。也就是说，有多少个$i$满足$ri\equiv0(\mod p-1)$，即$p-1\mid ri$。

令$d=\gcd(p-1,r)$，那么就得到$\dfrac{p-1}{d}\mid i$。因此，这样的$i$一共有$d$个。

回到原来的题目，那么关于$m$的方程$m^{e-1}\equiv 1(\mod p)$一共有$\gcd(p-1,e-1)$个解。

利用中国剩余定理的思想，并加上$m=0$的情况，关于$m$的方程$m^e\equiv m(\mod n)$一共有$(1+\gcd(p-1,e-1))(1+\gcd(q-1,e-1))$个解。

一个优化：由于$\gcd(e,\varphi)=1$，因此$e$必须是奇数。所以对于上面的式子而言，$\gcd(p-1,e-1),\gcd(q-1,e-1)$的值至少为$2$。可以发现将会存在$e$满足这两个$\gcd$的值都为$2$。

更进一步的优化：事先寻找出所有模$p-1(q-1)$为$2$的值，然后通过中国剩余定理进行合并。此处不详述这个优化。

## 代码

```C++
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const int P=1009,Q=3643;
int n=P*Q,phi=(P-1)*(Q-1);
int main(){
    ll ans=0;
    for(int e=2;e<phi;e++)
        if(__gcd(e,phi)==1&&__gcd(e-1,P-1)==2&&__gcd(e-1,Q-1)==2)
            ans+=e;
    printf("%lld\n",ans);
}

```
