---
title: Project Euler 650
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 650
## 题目
### Divisors of Binomial Product



Let $B(n) = \displaystyle \prod_{k=0}^n {n \choose k}$, a product of binomial coefficients.

For example, $B(5) = {5 \choose 0} \times {5 \choose 1} \times {5 \choose 2}  \times {5 \choose 3} \times {5 \choose 4} \times {5 \choose 5} = 1 \times 5 \times 10 \times 10 \times 5 \times 1 = 2500$.

Let $D(n) = \displaystyle \sum_{d|B(n)} d$, the sum of the divisors of $B(n)$.


For example, the divisors of $B(5)$ are $1, 2, 4, 5, 10, 20, 25, 50, 100, 125, 250, 500, 625, 1250$ and $2500$,

so $D(5) = 1 + 2 + 4 + 5 + 10 + 20 + 25 + 50 + 100 + 125 + 250 + 500 + 625 + 1250 + 2500 = 5467$.


Let $S(n) = \displaystyle \sum_{k=1}^n D(k)$.

You are given $S(5) = 5736$, $S(10) = 141740594713218418$ and $S(100) \mod 1\,000\,000\,007 = 332792866$.


Find $S(20\,000) \mod 1\,000\,000\,007$.





## 解决方案
根据组合数的定义，不难计算出

$$B(n)=\dfrac{(n!)^{n+1}}{\prod_{i=0}^n (i!)^2}$$

那么，不难将$B(n)$可以写成一个递推式：

$$B(n)=B(n-1)\cdot \dfrac{n^n}{n!}$$

直接维护$B(n)$的分解质因数$B(n)=p_1^{e_1}\cdot p_2^{e_2}\cdot p_1^{e_3}\dots$中$e_1,e_2,e_3\dots$的值。每一次求好之后利用因数和定理$\sigma(B(n))=\prod\dfrac{p_i^{e_i+1}-1}{p_i-1}$和快速幂算法进行计算。

## 代码


```C++
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N=20000;
bool vis[N+4];
int p[24],e[24],o=0;
int pr[N/10+1000],m=0;
ll mod=1e9+7;

void fact(int n){
    o=0;
    for(int i=1;i<=m&&pr[i]*pr[i]<=n;i++)
        if(n%pr[i]==0){
            p[++o]=pr[i];e[o]=0;
            for(;n%pr[i]==0;n/=pr[i],++e[o]);
        }
    if(n!=1){
        p[++o]=n;e[o]=1;
    }
}
ll qpow(ll n,ll m){
    ll a=1;
    for(;m;m>>=1){
        if(m&1) a=a*n%mod;
        n=n*n%mod;
    }
    return a;
}
int fac_fact[N+4],now_fact[N+4];
ll inv_p_1[N+4];
int main(){
    for(int i=2;i<=N;i++){
        if(vis[i]) continue;
        pr[++m]=i;
        for(ll j=1ll*i*i;j<=N;j+=i)
            vis[j]=true;
    }
    for(int i=1;i<=m;i++)
        inv_p_1[pr[i]]=qpow(pr[i]-1,mod-2);
    ll ans=0;
    for(int i=1;i<=N;i++){
        fact(i);
        for(int j=1;j<=o;j++) {
            fac_fact[p[j]]+=e[j];
            now_fact[p[j]]+=e[j]*i;
        }
        ll s=1;
        for(int j=1;j<=m&&pr[j]<=i;j++){
            now_fact[pr[j]]-=fac_fact[pr[j]];
            s=s*(qpow(pr[j],now_fact[pr[j]]+1)-1)%mod*inv_p_1[pr[j]]%mod;
        }
        ans=(ans+s)%mod;
    }
    printf("%lld\n",ans);
}
```