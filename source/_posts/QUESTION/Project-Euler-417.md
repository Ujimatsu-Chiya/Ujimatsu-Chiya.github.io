---
title: Project Euler 417
category:
  - Project Euler
tags:
mathjax: true
date: 2022-07-27 23:49:55
---

<escape><!-- more --></escape>

# Project Euler 417

## 题目

### Reciprocal cycles II

A unit fraction contains 1 in the numerator. The decimal representation of the unit fractions with denominators 2 to 10 are given:

$\begin{aligned}
&\dfrac{1}{2}=0.5\\
&\dfrac{1}{3}=0.(3)\\
&\dfrac{1}{4}=0.25\\
&\dfrac{1}{5}=0.2\\
&\dfrac{1}{6}=0.1(6)\\
&\dfrac{1}{7}=0.(142857)\\
&\dfrac{1}{8}=0.125\\
&\dfrac{1}{9}=0.(1)\\
&\dfrac{1}{10}=0.1\\
\end{aligned}$

Where $0.1(6)$ means $0.166666\dots$, and has a $1$-digit recurring cycle. It can be seen that $\dfrac{1}{7}$ has a $6$-digit recurring cycle.

Unit fractions whose denominator has no other prime factors than $2$ and/or $5$ are not considered to have a recurring cycle.

We define the length of the recurring cycle of those unit fractions as $0$.

Let $L(n)$ denote the length of the recurring cycle of $\dfrac{1}{n}$.

You are given that $\sum L(n)$ for $3 \le n \le 1 000 000$ equals $55535191115$.

Find $\sum L(n)$ for $3 \le n \le 100 000 000$.

## 解决方案

根据有理数上有理数的除法，不难发现，$L(n)=L(2n)=L(5n)$。那么本题我们仅需考虑$L(n)$，其中$2,5\nmid n$。

这个[页面](https://en.wikipedia.org/wiki/Repeating_decimal#Reciprocals_of_composite_integers_coprime_to_10)指出，如果$n$的分解质因数为$n=\prod_{i=1}^k p_i^{e_i}$，那么$L(n)=\text{lcm}(L(p_1^{e_1}),L(p_2^{e_2}),\dots,L(p_k^{e_k}))$。此外，这个页面还提到，绝大多数情况下，$L(p^e)=p\cdot L(p^{e-1})$，除了$p^e=3,487,56598313$这几个数（OEIS页面为[A045616](https://oeis.org/A045616)），这是因为$p^2\mid 10^{p-1}-1$。

那么现在问题就是求$L(p)$，其中$p$是不为$2,5$的质数。本质上，$L(p)$的值相当于元素$10$在乘法群$\mathbb{Z}_p^{\ast}$上的阶$\lambda_p(10)$。因此，一开始假设$\lambda_p(10)=p-1$。枚举$p-1$的每个质因子$q$，尝试对$\lambda_p(10)$除$q$。当发现$10^{\lambda_p(10)}\%p$不为$1$时，保留原来的值并停止。

## 代码

```C++
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N=100000000;
int v[N+4],pr[N/10+1000],m=0;
int L[N+4];
ll qpow(ll n,ll m,ll mod){
    ll a=1;
    for(;m;m>>=1){
        if(m&1) a=a*n%mod;
        n=n*n%mod;
    }
    return a;
}
int main(){
    for(int i=2;i<=N;i++){
        if(v[i]==0){
            v[i]=i;pr[++m]=i;
        }
        for(int j=1;j<=m;j++){
            if(pr[j]>v[i]||pr[j]>N/i) break;
            v[i*pr[j]]=pr[j];
        }
    }
    ll ans=0;
    for(int n=3;n<=N;n++){
        int m=n;
        for(;m%2==0;m>>=1);
        for(;m%5==0;m/=5);
        if(m<n) L[n]=L[m];
        else{
            if(v[n]==n){
                L[n]=n-1;
                ll x=n-1;
                for(;x!=1;){
                    int p=v[x];
                    for(;x%p==0;x/=p);
                    for(;L[n]%p==0&&qpow(10,L[n]/p,n)==1;L[n]/=p);
                }
            }else{
                int p=v[m];
                for(;m%p==0;m/=p);
                if(m==1&&(n/p==3||n/p==487)) L[n]=L[n/p];
                else if(m==1) L[n]=L[n/p]*p;
                else L[n]=lcm(L[m],L[n/m]);
            }
        }
        ans+=L[n];
    }
    printf("%lld\n",ans);

}

```
