---
title: Project Euler 272
tags:
  - Project Euler
  - OEIS
mathjax: true
date: 2022-07-27 23:49:36
---

<escape><!-- more --></escape>

# Project Euler 272

## 题目

### Modular Cubes, part 2

For a positive number $n$, define $C(n)$ as the number of the integers $x$, for which $1<x<n$ and $x^3\equiv 1 \mod n$.

When $n=91$, there are $8$ possible values for $x$, namely : $9, 16, 22, 29, 53, 74, 79, 81$.

Thus, $C(91)=8$.

Find the sum of the positive numbers $n\le10^{11}$ for which $C(n)=242$.

## 解决方案

枚举$n$，直接暴力求取前一部分$n$的该方程的解的个数，在OEIS中查询，发现结果为[A060839](https://oeis.org/A060839)。在FORMULA一栏中发现如下内容：

```
Let b(n) be the number of primes dividing n which are congruent to 1 mod 3 (sequence A005088); then a(n) is 3^b(n) if n is not divisible by 9 and 3^(b(n) + 1) if n is divisible by 9.
```

也就是说，对于$n$的分解质因数$n=\prod_{i=1}^k p_i^{e_i}$而言。假设有$b$个$p_i$模$3$余$1$的质因子。如果$n$是$9$的倍数，那么方程$x^3 \equiv1(\mod n)$有$3^{b+1}$个解，否则为$3^b$个。也就是

题目中问的是$242$，加上解$1$，那么实际上是询问$243=3^5$个解的情况，那么此处分开讨论$n$是否为$9$的倍数的情况。

首先通过线性筛，将所有质因子只包含模$3$余$2$的数筛选出来，存在集合$Q_2$中，在这个过程中也过滤出模$3$余$1$的质数，存在集合$P_1$中。前$4$个模$3$余$1$的质数分别是：$7,13,19,31$。那么，进行组合枚举时，枚举的最大质数将不超过$M=\max\lfloor(\dfrac{N}{\max(9,31)\cdot7\cdot 13,19}\rfloor,31)$。此处的$M$不大。因此线性筛的最大范围为$M$。

接下来先枚举$n$的质因数$3$的指数$e$。当$e<2$时，那么对$P_1$进行$b$个元素的组合枚举，枚举出它们的乘积$3^e\cdot p_1\cdot p_2\cdot ...\cdot p_b$。那么再将这个数和集合$Q_2$中的数一一组合，就能构造出一个个答案。当$e\ge2$时也类似。

## 代码

```C++
# include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const ll N=100000000000;
const int Q=242;
const int O=log(Q+1)/log(3)+1e-8;
const ll M=N/7/13/19/9+200;
int vis[M+4];
int pr[M/10+1000],m=0;
ll v[M+4];
ll ans=0,s[M+4];
void dfs(int f,int pos,ll n){
    if(f==0){
        ans+=s[N/n]*n;
        return;
    }
    for(int i=pos;i<=m;i++){
        ll ok=n;
        for(int k=0;k<f&&i+k<=m&&ok<=N;k++)
            ok*=pr[i+k];
        if(ok>N) break;
        for(ll k=n*pr[i];k<=N;k*=pr[i])
            dfs(f-1,i+1,k);
    }
}
int main(){
    s[1]=1;
    for(int i=2;i<=M;i++){
        if(v[i]==0){
            v[i]=i;pr[++m]=i;
            s[i]=(i%3==2);
        }
        for(int j=1;j<=m;j++){
            if(pr[j]>v[i]||pr[j]>M/i) break;
            v[i*pr[j]]=pr[j];
            s[i*pr[j]]=pr[j]%3==2?s[i]:0;
        }
    }
    int t=m;m=0;
    for(int i=1;i<=t;i++)
        if(pr[i]%3==1) pr[++m]=pr[i];
    for(int i=1;i<=M;i++)
        s[i]=s[i-1]+s[i]*i;
    dfs(O,1,1);dfs(O,1,3);
    for(ll k=9;k<=N;k*=3)
        dfs(O-1,1,k);
    printf("%lld\n",ans);
}

```
