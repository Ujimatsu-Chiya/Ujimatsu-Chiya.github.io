---
title: Project Euler 530
tags:
  - Project Euler
  - 数论分块
mathjax: true
date: 2022-08-05 21:40:45
---

<escape><!-- more --></escape>

# Project Euler 530

## 题目

### GCD of Divisors

Every divisor $d$ of a number $n$ has a **complementary divisor** $\dfrac{n}{d}$.

Let $f(n)$ be the sum of the **greatest common divisor** of $d$ and $\dfrac{n}{d}$ over all positive divisors d of n, that is $f(n)=\displaystyle\sum\limits_{d|n} \gcd(d,\frac n d)$.

Let $F$ be the summatory function of $f$, that is $F(k)=\displaystyle\sum\limits_{n=1}^k f(n)$.

You are given that $F(10)=32$ and $F(1000)=12776$.

Find $F(10^{15})$.

## 解决方案

令$N=10^{15}$。那么$F(N)$相当于是求所有$a,b$满足$ab\le k$的$\gcd(a,b)$之和，也就是：

$$F(N)=\sum_{i=1}^N \sum_{j=1}^{\lfloor\frac{N}{i}\rfloor} \gcd(i,j)=\sum_{d=1}^{\lfloor\sqrt{N}\rfloor} d\cdot S(\dfrac{n}{d})$$

其中，$S(n)$表示有多少对$i,j$，满足$ij\le n\wedge \gcd(i,j)=1$。

那么就可以写出如下等式：

$$\begin{aligned}
\sum_{i=1}^n \lfloor\dfrac{n}{i}\rfloor&=|\{(a,b)|ab\le n\}|\\
&=\sum_{d=1}^{\sqrt{n}}|\{(a,b)|ab\le n,\gcd(a,b)=d\}|\\
&=\sum_{d=1}^{\sqrt{n}}|\{(a,b)|ab\le \lfloor\dfrac{n}{d^2}\rfloor,\gcd(a,b)=1\}|\\
&=\sum_{d=1}^{\sqrt{n}}S(\dfrac{n}{d^2})
\end{aligned}$$

因此，可以得到关于$S$的递归式：

$$S(n)=\sum_{i=1}^n \lfloor\dfrac{n}{i}\rfloor-\sum_{d=2}^{\sqrt{n}}S(\dfrac{n}{d^2})$$

因此计算$S(n)$时，式子的第一个项，使用数论分块即可完成计算，而第二个项则直接暴力枚举。

正式计算$F(n)$时，同样直接枚举每一个项并相加即可。

## 代码

```C++
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;

const ll N=1000000000000000;
const int M=pow(N,0.52)+4;

unordered_map<ll,ll>mp;
int v[M+4],pr[M/5+1000],m=0;
int s[M+4];
ll cal(ll n){
    if(n<=M) return s[n];
    if(mp.count(n)) return mp[n];
    ll ans=0;
    for(ll l=1,r;l<=n;l=r+1){
        r=n/(n/l);
        ans+=n/l*(r-l+1);
    }
    for(ll l=2;l*l<=n;l++)
        ans-=cal(n/(l*l));
    return mp[n]=ans;
}
int main(){
    s[1]=1;
    for(int i=2;i<=M;i++){
        if(v[i]==0){
            v[i]=i;pr[++m]=i;s[i]=2;
        }
        for(int j=1;j<=m;j++){
            if(pr[j]>v[i]||pr[j]>M/i) break;
            v[i*pr[j]]=pr[j];
            s[i*pr[j]]=(pr[j]==v[i]?s[i]:s[i]*2);
        }
        s[i]+=s[i-1];
    }
    ll ans=0;
    for(ll l=1;l*l<=N;l++)
        ans+=l*cal(N/(l*l));
    printf("%lld\n",ans);
}

```
