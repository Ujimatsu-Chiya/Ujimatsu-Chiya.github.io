---
title: Project Euler 421
category:
  - Project Euler
tags:
mathjax: true
date: 2022-08-05 21:41:08
---

<escape><!-- more --></escape>

# Project Euler 421

## 题目

### Prime factors of $n^{15}+1$

Numbers of the form $n^{15}+1$ are composite for every integer $n > 1$.

For positive integers $n$ and $m$ let $s(n,m)$ be defined as the sum of the *distinct* prime factors of $n^{15}+1$ not exceeding $m$.

E.g. $2^{15}+1 = 3\times3\times11\times331$.

So $s(2,10) = 3$ and $s(2,1000) = 3+11+331 = 345$.

Also $10^{15}+1 = 7\times11\times13\times211\times241\times2161\times9091$.

So $s(10,100) = 31$ and $s(10,1000) = 483$.

Find $\sum s(n,10^8)$ for $1 \le n \le 10^{11}$.

## 解决方案

令$N=10^{11},M=10^8,K=15$。

求群$\mathbb{Z}_p^{\star}$的原根非常简单：从$2$开始枚举$g$，一个个进行判定。

判断一个元素$g$是否为$\mathbb{Z}_p^{\star}$的原根方法也比较简单：枚举$\varphi(p)=p-1$的所有质因数$k$，如果存在$k$使得$g^{\frac{p-1}{k}}\equiv 1(\mod p)$，那么$g$就不是原根，否则$g$是原根。

由于群$\mathbb{Z}_p^{\star}$有$\varphi(p-1)$个原根，因此实际上这种枚举原根的方法并不慢。

回到本问题，本质上是枚举质数$p$，然后判断方程$n^{K}\equiv -1(\mod p)$有多少个解小于等于$N$。为不失一般性，这里真正计算的解都小于$p$。

首先考虑方程$n^{K}\equiv 1(\mod p)$ 的解。令$n=g^i$，其中$g$是群$\mathbb{Z}_p^{\star}$上的原根，那么方程就化为：

$$g^{K\cdot i}\equiv g^0(\mod p)\qquad(1)$$

那么就可以写成

$$Ki\equiv 0(\mod p-1)\qquad(2)$$

令$d=\gcd(K,p-1)$。那么不难发现，方程$(2)$的所有解满足$\dfrac{p-1}{d}\cdot j$，其中$j=0,1,\dots,d-1.$

因此，令$h\equiv g^{\frac{p-1}{d}}(\mod p)$，那么方程$(1)$的解为$h^j$，其中$j=0,1,\dots,d-1.$

为了解回原方程$n^{K}\equiv -1(\mod p)$，那么首先判断$\dfrac{p-1}{d}$是否为偶数。如果不是，那么原方程无解（注意到这里$K=15$，因此$d$必为奇数，因此原方程必定有解，无需判断）；如果是，令$l=g^{\frac{p-1}{2d}}$，那么原方程的解为$l\cdot h^j$，其中$j=0,1,\dots,d-1$。

枚举方程$n^{K}\equiv -1(\mod p)$中的每个解$x$，那么这个解一共做出了$\lfloor\dfrac{N-x}{p}\rfloor+1$次贡献。

## 代码

```C++
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;

const ll N=100000000000;
const int M=100000000;
const int K=15;
int v[M+4],pr[M/10+1000],m=0;
ll qpow(ll n,ll m,ll p){
    ll a=1;
    for(;m;m>>=1){
        if(m&1) a=a*n%p;
        n=n*n%p;
    }
    return a;
}
int e[14],o=0;
int primitive_root(int p){
    if(p==2) return 1;
    int x=p-1;
    o=0;
    for(;x!=1;){
        int k=v[x];
        e[++o]=k;
        for(;x%k==0;x/=k);
    }
    for(int g=2;;g++){
        bool ok=1;
        for(int i=1;i<=o&&ok;i++)
            if(qpow(g,(p-1)/e[i],p)==1) ok=0;
        if(ok) return g;
    }
    return -1;
}
int main(){
    for(int i=2;i<=M;i++){
        if(v[i]==0){
            v[i]=i;pr[++m]=i;
        }
        for(int j=1;j<=m;j++){
            if(pr[j]>v[i]||pr[j]>M/i) break;
            v[i*pr[j]]=pr[j];
        }
    }
    ll ans=(N+1)/2*2;
    for(int i=2;i<=m;i++){
        int p=pr[i];
        int g=primitive_root(p);
        int d=__gcd(p-1,K);
        if(((p-1)/d)&1) continue;
        ll l=qpow(g,(p-1)/(2*d),p);
        ll h=qpow(g,(p-1)/d,p);
        ll x,t=1,cnt=0;
        for(int j=0;j<d;j++){
            x=l*t%p;
            t=t*h%p;
            cnt+=(N-x)/p+1;
        }
        ans+=cnt*p;
    }
    printf("%lld\n",ans);
}

```
