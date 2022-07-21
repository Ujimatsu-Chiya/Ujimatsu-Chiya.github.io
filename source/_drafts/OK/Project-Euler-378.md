---
title: Project Euler 378
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 378
## 题目
### Triangle Triples


Let $T(n)$ be the $n^\text{th}$ triangle number, so $T(n) = \dfrac{n(n + 1)}{2}$.

Let $dT(n)$ be the number of divisors of $T(n)$.

E.g.: $T(7) = 28$ and $dT(7) = 6$.

Let $Tr(n)$ be the number of triples $(i, j, k)$ such that $1 \le i \lt j \lt k \le n$ and $dT(i) \gt dT(j) \gt dT(k)$

$Tr(20) = 14$, $Tr(100) = 5772$, and $Tr(1000) = 11174776$.

Find $Tr(60 000 000)$. 

Give the last $18$ digits of your answer.




## 解决方案


## 代码


```C++
#include <bits/stdc++.h>
# define lb(i) ((i)&(-i))
typedef long long ll;
using namespace std;
const int N=60000000;
ll mod=1e18;
int M=0;
int v[N+4],pr[N/10+100],m=0;
int d[N+4];
ll s[N+4],f[N+4];
void add(int p,ll x){
    for(int i=p;i<=M;i+=lb(i)){
        s[i]=(s[i]+x)%mod;
    }
}
ll que(int p){
    ll a=0;
    for(int i=p;i;i-=lb(i))
        a=(a+s[i])%mod;
    return a;
}
int main(){
    f[1]=1;
    for(int i=2;i<=N+1;i++){
        if(v[i]==0){
            v[i]=i;pr[++m]=i;f[i]=2;
        }
        for(int j=1;j<=m;j++){
            if(pr[j]>v[i]||pr[j]>(N+1)/i) break;
            v[i*pr[j]]=pr[j];
            f[i*pr[j]]=f[i]*2-(pr[j]==v[i]?f[i/pr[j]]:0);
        }
    }
    for(int n=1;n<=N;n++)
        d[n]=n&1?f[n]*f[(n+1)>>1]:f[n>>1]*f[n+1];
    M=*max_element(d+1,d+N+1);
    for(int i=1;i<=N;i++)
        f[i]=1;
    for(int k=1;k<=2;k++){
        memset(s,0,sizeof(s));
        ll sum=0;
        for(int i=1;i<=N;i++){
            ll x=f[i];
            f[i]=sum-que(d[i]);
            add(d[i],x);
            sum+=x;
        }
    }
    ll ans=0;
    for(int i=1;i<=N;i++)
        ans=(ans+f[i])%mod;
    printf("%lld\n",ans);
}

```