---
title: Project Euler 429
tags:
  - Project Euler
mathjax: true
date: 2022-06-05 09:28:44
---

<escape><!-- more --></escape>

# Project Euler 429

## 题目

### Sum of squares of unitary divisors

A unitary divisor $d$ of a number $n$ is a divisor of $n$ that has the property $\gcd(d, \dfrac{n}{d}) = 1$.

The unitary divisors of $4! = 24$ are $1, 3, 8$ and $24$.

The sum of their squares is $1^2 + 3^2 + 8^2 + 24^2 = 650$.

Let $S(n)$ represent the sum of the squares of the unitary divisors of $n$. Thus $S(4!)=650$.

Find $S(100 000 000!) \text{ modulo } 1 000 000 009$.

## 解决方案

如果一个正整数$n$分解后成为：

$$n=\prod_{i=1}^m p_i^{e_i}$$

对于$n$的某个因子$d=\prod_{i=1}^mp_i^{e_i'}$而言，如果$\gcd(d,\dfrac{n}{d})=1$，那么对于所有$i\in [1,m]$，都有$e_i'\in\{0,e_i\} $。

原因：如果$d$的一个质因子$p_i$的指数$e_i'\notin\{0,e_i\}$，也就是$0<e_i'<e_i$，那么$\dfrac{n}{d}$对应下的质因子的指数为$0<e_i-e_i'<e_i$，因此$\gcd(d,\dfrac{n}{d})$一定是$p_i$的倍数，所以原来的命题成立。

这些因子一共有$2^m$个，因为对于所有$i\in [1,m]$，$e_i'$都有两个选择。因此，这$2^m$个因子的平方和为：

$$S(n)=\prod_{i=1}^m(p_i^{2e_i}+1)$$

另一个问题则是：$n!$中质因子$p$出现了多少次？

设$f(n, p)$是质因子$p$在$n!$中的次数，那么$f(n,p)=\lfloor\dfrac{n}{p}\rfloor+\lfloor\dfrac{n}{p^2}\rfloor+\lfloor\dfrac{n}{p^3}\rfloor+\dots$，每一项分别表示$1\sim n$中有多少个数是$p,p^2,p^3\dots$的倍数。

最终，将这$2$个过程相结合，直接计算$S(N!)$的值，其中$N=10^8$。

## 代码

```C++
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N=1e8;
ll mod=1e9+9;
ll qpow(ll n,ll m){
    ll ans=1;
    for(;m;m>>=1){
        if(m&1) ans=ans*n%mod;
        n=n*n%mod;
    }
    return ans;
}
int cal(int n,int p){
    int ans=0;
    for(;n;n/=p)
        ans+=n/p;
    return ans;
}
int pr[N+4],v[N+4],m=0;
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
    ll ans=1;
    for(int i=1;i<=m;i++){
        ll cnt=cal(N,pr[i]);
        ans=ans*(qpow(pr[i],cnt*2)+1)%mod;
    }
    printf("%lld\n",ans);
}

```
