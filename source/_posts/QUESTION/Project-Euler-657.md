---
title: Project Euler 657
tags:
  - 容斥原理
category:
  - Project Euler
mathjax: true
date: 2022-08-21 23:51:08
---

<escape><!-- more --></escape>

# Project Euler 657

## 题目

### Incomplete words

In the context of **formal languages**, any finite sequence of letters of a given **alphabet** $\Sigma$ is called a **word** over $\Sigma$. We call a word *incomplete* if it does not contain every letter of $\Sigma$.

For example, using the alphabet $\Sigma=\{ a, b, c\}$, '$ab$', '$abab$' and '$\,$' (the empty word) are incomplete words over $\Sigma$, while '$abac$' is a complete word over $\Sigma$.

Given an alphabet $\Sigma$ of $\alpha$ letters, we define $I(\alpha,n)$ to be the number of incomplete words over $\Sigma$ with a length not exceeding $n$.

For example, $I(3,0)=1$, $I(3,2)=13$ and $I(3,4)=79$.

Find $I(10^7,10^{12})$. Give your answer modulo $1\,000\,000\,007$.

## 解决方案

令$N=10^7,M=10^{12}$。考虑使用容斥原理解决本题。

如果当前只使用其中$i$个字母，那么单词的数量个数$f_{N,M}(i)$如下：

$$f_{N,M}(i)\dbinom{N}{i}\sum_{j=0}^{M} i^j$$

这是一个很明显的等比数列求和式，但是当$i=1$时，式子不适用等比数列求和公式，因此化简成$N\cdot (M+1)$。否则可以化简成$\dbinom{N}{i}\cdot \dfrac{i^{M+1}-1}{i-1}$

注意到$f_{N,M}(N-1)$中的一些单词实际上有单词使用了$N-2$个字母，因此需要减去$f_{N,M}(N-2)$的情况，而使用$N-3$个字母的单词被重复减去了，需要加上……

最终，$I$可以写成：

$$I(N,M)=\sum_{i=0}^{N-1}(-1)^{N-1-i}\cdot f_{N,M}(i)$$

## 代码

```C++
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N=10000000;
const ll M=1000000000000;
ll mod=1000000007;
ll fac[N+4],inv[N+4],finv[N+4];
ll C(int n,int m){
    return fac[n]*finv[n-m]%mod*finv[m]%mod;
}
ll qpow(ll n,ll m){
    m%=mod-1;
    ll a=1;
    for(;m;m>>=1){
        if(m&1) a=a*n%mod;
        n=n*n%mod;
    }
    return a;
}
int main(){
    fac[0]=fac[1]=inv[1]=finv[0]=finv[1]=1;
    for(int i=2;i<=N;i++){
        fac[i]=fac[i-1]*i%mod;
        inv[i]=(mod-mod/i)*inv[mod%i]%mod;
        finv[i]=finv[i-1]*inv[i]%mod;
    }
    ll ans=0;
    for(int i=N-1,f=1;i>=0;i--,f=-f){
        if(i==0) ans+=f;
        else if(i==1) ans+=(M+1)%mod*N%mod*f;
        else ans+=C(N,i)*(qpow(i,M+1)-1)%mod*inv[i-1]%mod*f;
    }
    ans=(ans%mod+mod)%mod;
    printf("%lld\n",ans);
}

```
