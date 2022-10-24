---
title: Project Euler 602
category:
  - Project Euler
mathjax: true
  - 概率
date: 2022-08-21 23:51:34
tags:
---

<escape><!-- more --></escape>

# Project Euler 602

## 题目

### Product of Head Counts

Alice enlists the help of some friends to generate a random number, using a single unfair coin. She and her friends sit around a table and, starting with Alice, they take it in turns to toss the coin. Everyone keeps a count of how many heads they obtain individually. The process ends as soon as Alice obtains a Head. At this point, Alice multiplies all her friends' Head counts together to obtain her random number.

As an illustration, suppose Alice is assisted by Bob, Charlie, and Dawn, who are seated round the table in that order, and that they obtain the sequence of Head/Tail outcomes **THHH—TTTT—THHT—H** beginning and ending with Alice. Then Bob and Charlie each obtain $2$ heads, and Dawn obtains $1$ head. Alice's random number is therefore $2\times 2\times 1 = 4$.

Define $e(n, p)$ to be the expected value of Alice's random number, where $n$ is the number of friends helping (excluding Alice herself), and $p$ is the probability of the coin coming up Tails.

It turns out that, for any fixed $n$, $e(n, p)$ is always a polynomial in $p$. For example, $e(3, p) = p^3 + 4p^2 + p$.

Define $c(n, k)$ to be the coefficient of $p^k$ in the polynomial $e(n, p)$. So $c(3, 1) = 1$, $c(3, 2) = 4$, and $c(3, 3) = 1$.

You are given that $c(100, 40) \equiv 986699437 \text{ } (\text{mod } 10^9+7)$.

Find $c(10000000, 4000000) \bmod 10^9+7$.

## 解决方案

不难直接写出关于$e(n,p)$的定义式：

$$\begin{aligned}
e(n,p)&=\sum_{k=1}^{\infty} p^k \cdot (1-p) \cdot (k\cdot (1-p))^n\\
&=\sum_{k=1}^{\infty} p^k \cdot k^n\cdot (1-p)^{n+1}\\
&=(1-p)^{n+1}\cdot \sum_{k=1}^{\infty} p^k \cdot k^n
\end{aligned}$$

其中，枚举变量$k$表示Alice已经连续抛出了$k$次反面，在第$k+1$次抛出了正面，游戏结束。而$k$个人分别是在做独立的伯努利实验，因此他们每一个人抛出正面的次数期望为$k\cdot(1-p)$。

那么根据二项式定理，左边可以展开成：

$$(1-p)^{n+1}=\sum_{k=0}^{n+1} (-1)^k\cdot \dbinom{n+1}{k}p^k$$

和右边的多项式相乘，保留第$k$项的系数，因此有：

$$c(n,m)=\sum_{k=0}^{m-1} (-1)^k\cdot \dbinom{n+1}{k} \cdot (m-k)^n$$

## 代码

```C++
# include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N=10000000,M=4000000;
ll fac[N+4],finv[N+4],mod=1e9+7;
ll qpow(ll n,ll m){
    ll a=1;
    for(;m;m>>=1){
        if(m&1) a=a*n%mod;
        n=n*n%mod;
    }
    return a;
}
ll C(int n,int m){
    return fac[n]*finv[n-m]%mod*finv[m]%mod;
}
int main(){
    fac[0]=1;
    for(int i=1;i<=N+1;i++){
        fac[i]=fac[i-1]*i%mod;
    }
    finv[N+1]=qpow(fac[N+1],mod-2);
    for(int i=N;i>=0;i--)
        finv[i]=finv[i+1]*(i+1)%mod;
    ll ans=0;
    for(int k=0,f=1;k<M;k++,f=-f)
        ans+=C(N+1,k)*qpow(M-k,N)*f%mod;
    ans=(ans%mod+mod)%mod;
    printf("%lld\n",ans);
}

```
