---
title: Project Euler 625
category:
  - Project Euler
tags:
  - 数论分块
mathjax: true
date: 2022-06-13 21:21:46
---

<escape><!-- more --></escape>

# Project Euler 625

## 题目

### Gcd sum

$G(N)=\sum_{j=1}^N\sum_{i=1}^j \text{gcd}(i,j)$.

You are given: $G(10)=122$.

Find $G(10^{11})$. Give your answer modulo $998244353$.

## 解决方案

令$\Phi(n)=\sum_{i=1}^n\varphi(n)$，其中$\varphi$为欧拉函数。

$$\begin{aligned}
G(N)&=\sum_{j=1}^N\sum_{i=1}^j \text{gcd}(i,j)=\sum_{g=1}^Ng\sum_{j=1}^N\sum_{i=1}^j[\gcd(i,j)=g] \\
&=\sum_{g=1}^Ng\sum_{j=1}^N\sum_{i=1}^j[\gcd(i,j)=g] \\
&=\sum_{g=1}^Ng\sum_{j=1}^{\left\lfloor\frac{N}{g}\right\rfloor}\sum_{i=1}^j[\gcd(i,j)=1]\\
&=\sum_{g=1}^Ng\sum_{j=1}^{\left\lfloor\frac{N}{g}\right\rfloor}\varphi(i)\\
&=\sum_{g=1}^Ng\Phi\left(\dfrac{N}{g}\right)
\end{aligned}$$

其中，$[]$表示示性函数，表示$[]$里面的值是否为真，如果为真，那么值为$1$，否则值为$0$.

这启发我们使用数论分块进行解决。考虑两层嵌套的数论分块，外层的计算$g(n)$的值，内层的计算$\Phi(n)$的值。

那么现在的问题就是使用数论分块的方法高效计算$\Phi(n)$的值。

$$\begin{aligned}
\dfrac{n(n+1)}{2}&=|\{(a,b)|1\le a\le b \le n\}|\\
&=\sum_{d=1}^n|\{(a,b)|1\le a\le b \le n,\gcd(a,b)=d\}|\\
&=\sum_{d=1}^n\left|\left\{(a,b)| 1\le a\le b \le \left\lfloor\dfrac{n}{d}\right\rfloor,\gcd(a,b)=1\right\}\right|\\
&=\sum_{d=1}^n\Phi\left(\dfrac{n}{d}\right)
\end{aligned}$$

因此，可以得到关于$\Phi$的递归式：

$$\Phi(n)=\dfrac{n(n+1)}{2}-\sum_{d=2}^n\Phi\left(\dfrac{n}{d}\right)$$

## 代码

```C++
#include <bits/stdc++.h>
typedef long long ll;
using namespace std;
const ll N=1e11;
const ll mod=998244353;
const int M = pow(N, 2.0 / 3);
int s[M+4];
int v[M+4],pr[M/10+1000],m=0;
unordered_map<ll,ll>mp;
ll inv2= (mod+1)>>1;
ll sum_phi(ll n)
{
    if(n <= M) return s[n];
    if(mp.count(n)) return mp[n];
    ll ans= ((n + 1) % mod * (n % mod) % mod) * inv2 % mod;
    for(ll l=2,r; l <= n; l= r + 1)
    {
        r= n / (n / l);
        ans= (ans - (r - l + 1) % mod * sum_phi(n / l) % mod + mod) % mod;
    }
    return mp[n]=ans;
}
int main() {
    s[1]=1;
    for(int i=2;i<=M;i++) {
        if(v[i]==0){
            v[i]=i;pr[++m]=i;s[i]=i-1;
        }
        for(int j=1;j<=m;j++){
            if(pr[j]>v[i]||pr[j]>M/i) break;
            v[i*pr[j]]=pr[j];
            s[i*pr[j]]=s[i]*(pr[j]==v[i]?pr[j]:pr[j]-1);
        }
    }
    for(int i=2;i<=M;i++)
        s[i]=(s[i]+s[i-1])%mod;
    ll ans=0;
    for(ll l=1,r;l<=N;l=r+1){
        r=N/(N/l);
        // l<=g<=r
        ans=(ans+(l+r)%mod*((r-l+1)%mod)%mod*inv2%mod*sum_phi(N/l)+mod)%mod;
    }
    printf("%lld\n",ans);
}

```
