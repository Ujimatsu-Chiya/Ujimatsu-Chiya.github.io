---
title: Project Euler 675
tags:
  - Project Euler
mathjax: true
date: 2022-07-17 23:11:18
---

<escape><!-- more --></escape>

# Project Euler 675

## 题目

### $2^{\omega(n)}$

Let $\omega(n)$ denote the number of distinct prime divisors of a positive integer $n$.

So  $\omega(1) = 0$ and  $\omega(360) = \omega(2^{3} \times 3^{2} \times 5) = 3$.

Let $S(n)$ be $\Sigma_{d | n} 2^{\omega(d)}$.

E.g. $S(6) = 2^{\omega(1)}+2^{\omega(2)}+2^{\omega(3)}+2^{\omega(6)} = 2^0+2^1+2^1+2^2 = 9$.

Let $F(n)=\Sigma_{i=2}^n S(i!)$.

$F(10)=4821$.

Find $F(10\,000\,000)$. Give your answer modulo  $1\,000\,000\,087$.

## 解决方案

假设$n$的分解为$\prod_{i=1}^kp_i^{e_i}$。

根据$\omega$函数的定义，当$\gcd(a,b)=1$时，有$\omega(ab)=\omega(a)+\omega(b)$，并且，$\omega(p_i^{e_i})=1$.

对于函数$S$而言，意味着每一项的$2^{\omega(ab)}$可以写成$2^{\omega(a)}\cdot 2^{\omega(b)}$。那么考虑$n$的某个质因数分量$p_i^{e_i}$，那么发现，$S$中的每个和式包含了$2^{\omega(p_i^0)},2^{\omega(p_i^1)},\dots,2^{\omega(p_i^{e_i})}$中的某一个项，并且发现这些项跟除$2^{\omega(p_i^j)}$以外的所有项都是一一组合。因此考虑将上面的这些项加起来，得到$(2e_i+1)$。

将每个分量进行同样的操作，最终得到$S(n)=\prod_{i=1}^k(2e_i+1)$。

由于本题计算的是$S(n!)$的前缀和，因此从小到大枚举$n$，并对$n$进行分解质因数。在整个过程中，用一个数组维护$n!$的分解质因数的结果，在此过程维护$S(n!)$的值。对于单独的一个$n$，如果使用线性逆元，那么维护成本为$O(\log n)$。

## 代码

```C++
# include <bits/stdc++.h>
# define pi pair<int,int>
using namespace std;
typedef long long ll;
const int N=10000000;
const int M=2*N+1;
ll mod=1000000087;
int pr[N/10+100],v[N+4],m=0;
int e[N+4];
ll inv[M+4];
int a[14],b[14],o=0;
void fact(int n){
    o=0;
    for(;n!=1;){
        a[++o]=v[n];
        b[o]=0;
        for(;n%a[o]==0;n/=a[o],++b[o]);
    }
}
int main(){
    for(int i=2;i<=N;i++){
        if(v[i]==0) pr[++m]=i,v[i]=i;
        for(int j=1;j<=m;j++){
            if(pr[j]>v[i]||pr[j]>N/i) break;
            v[i*pr[j]]=pr[j];
        }
    }
    inv[1]=1;
    for(int i=2;i<=M;i++)
        inv[i]=(mod-mod/i)*inv[mod%i]%mod;
    ll ans=0,v=1;
    for(int i=2;i<=N;i++){
        fact(i);
        for(int j=1;j<=o;j++){
            v=v*inv[2*e[a[j]]+1]%mod;
            e[a[j]]+=b[j];
            v=v*(2*e[a[j]]+1)%mod;
        }
        ans=(ans+v)%mod;
    }
    printf("%lld\n",ans);

}

```
