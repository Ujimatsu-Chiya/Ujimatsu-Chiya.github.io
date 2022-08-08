---
title: Project Euler 365
category:
  - Project Euler
tags:
  - 卢卡斯定理
  - 中国剩余定理
mathjax: true
date: 2022-07-12 00:17:10
---

<escape><!-- more --></escape>

# Project Euler 365

## 题目

### A huge binomial coefficient

The binomial coefficient $\displaystyle{\binom{10^{18}}{10^9}}$ is a number with more than 9 billion ($9\times 10^9$) digits.

Let $M(n,k,m)$ denote the binomial coefficient $\displaystyle{\binom{n}{k}}$ modulo $m$.

Calculate $\displaystyle{\sum M(10^{18},10^9,p\cdot q\cdot r)}$ for $1000\lt p\lt q\lt r\lt 5000$ and $p$,$q$,$r$ prime.

## 解决方案

令$pr$为所有满足$1000< p< 5000$的质数$p$的数组。

利用[卢卡斯定理](https://en.wikipedia.org/wiki/Lucas%27s_theorem)，可以预处理出所有$\displaystyle{\binom{10^{18}}{10^9}}\%p$的值。

再使用[中国剩余定理](https://mathworld.wolfram.com/ChineseRemainderTheorem.html)对任意三个质数下的解进行合并。

发现在这些质数$p$中，大多数都有$\displaystyle{\binom{10^{18}}{10^9}}\%p=0$。因此当枚举的三个质数都满足模$p$为$0$时，此时的解肯定为$0$，直接跳过。

## 代码

```C++
# include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const ll N=1e18,M=1e9;
const int L=1000,R=5000;
bool vis[R+4];
vector<int>pr,a;
int fac[R+4];
ll inv(ll n,ll p){
    ll a=1,m=p-2;
    for(;m;m>>=1){
        if(m&1) a=a*n%p;
        n=n*n%p;
    }
    return a;
}
ll CRT(ll *a,ll *p,int n){
    ll M=1;
    ll ans=0;
    for(int i=0;i<n;i++) M*=p[i];
    for(int i=0;i<n;i++)
        ans=(ans+a[i]*inv(M/p[i],p[i])*(M/p[i]))%M;
    return ans%M;
}
int C(int n,int m,int p){
    if(m>n) return 0;
    return fac[n]*inv(fac[m],p)%p*inv(fac[n-m],p)%p;
}
ll lucas(ll n,ll m,ll p){
    return n==0?1:C(n%p,m%p,p)*lucas(n/p,m/p,p)%p;
}
int main(){
    for(int i=2;i<R;i++){
        if(vis[i]) continue;
        if(i>L) pr.push_back(i);
        for(int j=i+i;j<R;j+=i)
            vis[j]=1;
    }
    for(int p:pr){
        fac[0]=1;
        for(int i=1;i<p;i++)
            fac[i]=fac[i-1]*i%p;
        a.push_back(lucas(N,M,p));
    }
    ll ans=0;
    for(int i=0;i<pr.size();i++)
        for(int j=0;j<i;j++)
            for(int k=0;k<j;k++)
                if(a[i]||a[j]||a[k]){
                    ll b[]={a[i],a[j],a[k]},p[]={pr[i],pr[j],pr[k]};
                    ans+=CRT(b,p,3);
                }

    printf("%lld\n",ans);
}

```

上面的代码运行时间略久，这是因为计算中国剩余定理的过程中总需要计算重新计算逆元。考虑一开始就将所有逆元线性预处理出来，那么整个程序运行时间下降到原来的约$\dfrac{1}{3}$。

```C++
# include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const ll N=1e18,M=1e9;
const int L=1000,R=5000;
bool vis[R+4];
vector<int>pr,a;
vector<vector<int>>inv_list;
int fac[R+4];
ll inv(ll n,ll p){
    ll a=1,m=p-2;
    for(;m;m>>=1){
        if(m&1) a=a*n%p;
        n=n*n%p;
    }
    return a;
}
ll CRT(ll *a,ll *p,int n){
    ll M=1;
    ll ans=0;
    for(int i=0;i<n;i++) M*=p[i];
    for(int i=0;i<n;i++)
        ans=(ans+a[i]*inv_list[p[i]][M/p[i]%p[i]]*(M/p[i]))%M;
    return ans%M;
}
int C(int n,int m,int p){
    if(m>n) return 0;
    return fac[n]*inv_list[p][fac[m]]%p*inv_list[p][fac[n-m]]%p;
}
ll lucas(ll n,ll m,ll p){
    return n==0?1:C(n%p,m%p,p)*lucas(n/p,m/p,p)%p;
}
int main(){
    inv_list.resize(R);
    for(int i=2;i<R;i++){
        if(vis[i]) continue;
        if(i>L){
            pr.push_back(i);
            inv_list[i].resize(i);
            inv_list[i][1]=1;
            for(int j=2;j<i;j++){
                inv_list[i][j]=(i-i/j)*inv_list[i][i%j]%i;
            }
        }
        for(int j=i+i;j<R;j+=i)
            vis[j]=1;
    }
    for(int p:pr){
        fac[0]=1;
        for(int i=1;i<p;i++)
            fac[i]=fac[i-1]*i%p;
        a.push_back(lucas(N,M,p));
    }
    ll ans=0;
    for(int i=0;i<pr.size();i++)
        for(int j=0;j<i;j++)
            for(int k=0;k<j;k++)
                if(a[i]||a[j]||a[k]){
                    ll b[]={a[i],a[j],a[k]},p[]={pr[i],pr[j],pr[k]};
                    ans+=CRT(b,p,3);
                }

    printf("%lld\n",ans);
}

```
