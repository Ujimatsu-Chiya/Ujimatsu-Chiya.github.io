---
title: Project Euler 193
category:
  - Project Euler
tags:
  - 容斥原理
mathjax: true
date: 2022-05-19 21:56:35
---

<escape><!-- more --></escape>

# Project Euler 193

## 题目

### Squarefree Numbers

A positive integer $n$ is called squarefree, if no square of a prime divides $n$, thus $1, 2, 3, 5, 6, 7, 10, 11$ are squarefree, but not $4, 8, 9, 12$.

How many squarefree numbers are there below $2^{50}$?

## 莫比乌斯函数

[莫比乌斯函数](https://en.wikipedia.org/wiki/M%C3%B6bius_function)，常用于容斥原理。

假设$n$的分解质因数为$n=p_1^{e_1}\cdot p_2^{e_2}\cdot \dots \cdot p_k^{e_k}$，那么莫比乌斯函数$\mu(n)$函数值定义如下：

$$
\mu(n)=
\left \{\begin{aligned}
  &1 & & \text{if}\quad n=1 \\
  &0 & & \text{else if}\quad \exists m\in[1,k],e_m>1 \\
  &(-1)^k & & \text{else}
\end{aligned}\right.
$$

## 解决方案

基于容斥原理的思想，我们首先假设所有数都是无平方因子数，然后减去有$1$个质因子的$e_i>1$的数。在此减去过程中，会有$2$两个质因子的$e_i>1$的质数被重复减去，因此需要补回。。。

为了不重不漏，有平方因子数完全不参与上面的过程。

那么发现，只要有偶数个质因子的就会被增加，有奇数个质因子就会被减去。莫比乌斯函数恰好帮助我们表示了整个过程。

使用线性筛计算莫比乌斯函数：如果筛出来的是一个新质因子，那么对原来的莫比乌斯函数值乘$-1$就可以得到新数的莫比乌斯函数值，如果是旧的质因子，那么直接赋$0$。

最终答案为：
$$\sum_{k=1}^{\lfloor\sqrt{N}\rfloor} \left\lfloor\dfrac{N}{k^2}\right\rfloor\cdot \mu(k)$$

## 代码

```C++
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const ll N=1ll<<50;
const ll M=sqrt(N);
int mu[M+1];
int pr[M+1],v[M+1],m=0;
int main(){
    mu[1]=1;
    for(int i=2;i<=M;i++){
        if(v[i]==0){
            pr[++m]=i;v[i]=i;
            mu[i]=-1;
        }
        for(int j=1;j<=m;j++){
            if(pr[j]>v[i]||pr[j]>M/i) break;
            v[i*pr[j]]=pr[j];
            mu[i*pr[j]]=(v[i]==pr[j]?0:-mu[i]);
        }
    }
    ll ans=0;
    for(int i=1;i<=M;i++)
        ans+=1ll*mu[i]*(N/(1ll*i*i));
    printf("%lld\n",ans);
}
```
