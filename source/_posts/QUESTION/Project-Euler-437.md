---
title: Project Euler 437
category:
  - Project Euler
tags:
mathjax: true
date: 2022-08-05 21:41:17
---

<escape><!-- more --></escape>

# Project Euler 437

## 题目

### Fibonacci primitive roots

When we calculate $8^n$ modulo $11$ for $n=0$ to $9$ we get: $1, 8, 9, 6, 4, 10, 3, 2, 5, 7$.

As we see all possible values from $1$ to $10$ occur. So $8$ is a **primitive root** of $11$.

But there is more:

If we take a closer look we see:

$\begin{aligned}
& 1+8=9\\
& 8+9=17\equiv6 \bmod 11\\
& 9+6=15\equiv4 \bmod 11\\
& 6+4=10\\
& 4+10=14\equiv3 \bmod 11\\
& 10+3=13\equiv2 \bmod 11\\
& 3+2=5\\
& 2+5=7\\
& 5+7=12\equiv1 \bmod 11.
\end{aligned}$

So the powers of $8$ mod $11$ are cyclic with period $10$, and $8^n + 8^{n+1} \equiv 8^{n+2} \pmod {11}$.

$8$ is called a **Fibonacci primitive root** of $11.$

Not every prime has a Fibonacci primitive root.

There are $323$ primes less than $10000$ with one or more Fibonacci primitive roots and the sum of these primes is $1480491$.

Find the sum of the primes less than $100,000,000$ with at least one Fibonacci primitive root.

## 解决方案

假设群$\mathbb{Z}_p^{\star}$上的一个原根为$g$，那么按照上面对斐波那契原根的定义，可以写成：

$\forall n,g^n+g^{n+1}-g^{n+2}\equiv 0\pmod p$

那么提取公因式，有$g^n(1+g-g^2)\equiv 0\pmod p$

由于$g$是原根，$g^n$永远不可能为$0$，因此转化为求$g^2-g-1\equiv 0\pmod p$

也就是$(2g-1)^2\equiv 5\pmod p$

解这个方程，如果找到了一个根$g$，那么不难发现$g'=p-g+1$是这个方程的另外一个根。

令$f(n)=n^2-n-1$，那么使用216题的分解方式对$f(n)$进行分解：如果$p\mid f(n)$，那么$p\mid f(kp+n),p\mid f(kp-n+1)$，其中$k>0$。那么最终若$f(n)$被筛剩一个质因子$p$，那么$n$就是方程$g^2-g-1\equiv 0\pmod p$的一个解。

判断一个元素$g$是否为$\mathbb{Z}_p^{\ast}$的原根方法也比较简单：枚举$\varphi(p)=p-1$的所有质因数$k$，如果存在$k$使得$g^{\frac{p-1}{k}}\equiv 1\pmod p$，那么$g$就不是原根，否则$g$是原根。

## 代码

```C++
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;

const int N=100000000;

ll f[N+4];
int v[N+4],pr[N/10+1000],m=0;
ll qpow(ll n,ll m,ll p){
    ll a=1;
    for(;m;m>>=1){
        if(m&1) a=a*n%p;
        n=n*n%p;
    }
    return a;
}
bool is_primitive_root(int g,int p){
    int x=p-1;
    for(;x!=1;){
        int k=v[x];
        if(qpow(g,(p-1)/k,p)==1) return 0;
        for(;x%k==0;x/=k);
    }
    return 1;
}
int main(){
    for(int i=1;i<=N;i++)
        f[i]=1ll*i*i-i-1;
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
    for(int i=3;i<N;i++){
        ll p=f[i];
        if(p==1||p>N) continue;
        if(is_primitive_root(i,p)||is_primitive_root(p-i+1,p)) ans+=p;
        for(int j=i;j<N;j+=p)
            for(;f[j]%p==0;f[j]/=p);
        for(int j=p-i+1;j<N;j+=p)
            for(;f[j]%p==0;f[j]/=p);
    }
    printf("%lld\n",ans);
}

```
