---
title: Project Euler 643
tags:
  - Project Euler
  - 数论分块
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 643
## 题目
### 2-Friendly


Two positive integers $a$ and $b$ are *$2$-friendly* when $\gcd(a,b) = 2^t, t>0$. For example, $24$ and $40$ are $2$-friendly because $\gcd(24,40) = 8 = 2^3$ while $24$ and $36$ are not because $\gcd(24,36) = 12 = 2^2\cdot 3$ not a power of $2$.

Let $f(n)$ be the number of pairs, $(p,q)$, of positive integers with $1\le p\lt q\le n$ such that $p$ and $q$ are $2$-friendly. You are given $f(10^2) = 1031$ and $f(10^6) = 321418433 \text{ modulo } 1\,000\,000\,007$.

Find $f(10^{11})\text{ modulo } 1\,000\,000\,007$.


## 解决方案

令$\Phi(n)=\sum_{i=1}^n\varphi(n)$，其中$\varphi$为欧拉函数。

那么$f(n)$定义并化简的步骤如下：

$$\begin{aligned}
f(n)&=\sum_{t=1}^{\lfloor \log_2n\rfloor}(-1+\sum_{q=1}^n\sum_{p=1}^{q}[\gcd(p,q)=2^t]) \\
&=\sum_{t=1}^{\lfloor \log_2n\rfloor}(-1+\sum_{q=1}^{\lfloor\frac{n}{2^t}\rfloor}\sum_{p=1}^{q}[\gcd(p,q)=1])\\
&=\sum_{t=1}^{\lfloor \log_2n\rfloor}(-1+\sum_{q=1}^{\lfloor\frac{n}{2^t}\rfloor}\varphi(q))\\
&=\sum_{t=1}^{\lfloor \log_2n\rfloor}(\Phi(\lfloor\frac{n}{2^t}\rfloor)-1)
\end{aligned}$$

和512题一样，现在的问题就是使用数论分块的方法高效计算$\Phi(n)$的值。

$$\begin{aligned}
\dfrac{n(n+1)}{2}&=|\{(a,b)|1\le a\le b \le n\}|\\
&=\sum_{d=1}^n\{(a,b)|1\le a\le b \le n,\gcd(a,b)=d\}|\\
&=\sum_{d=1}^n\{(a,b)|1\le a\le b \le \lfloor\dfrac{n}{d}\rfloor,\gcd(a,b)=1\}\\
&=\sum_{d=1}^n\Phi(\dfrac{n}{d})
\end{aligned}$$

因此，可以得到关于$\Phi$的递归式：

$$\Phi(n)=\dfrac{n(n+1)}{2}-\sum_{d=2}^n\Phi(\dfrac{n}{d})$$

其中，右边这一部分可以使用数论分块来解决。


## 代码


```C++
#include <bits/stdc++.h>
typedef long long ll;
using namespace std;
const ll N=1e11;
const ll mod=1000000007;
const int M = pow(N, 2.0 / 3);
int s[M+4];
int v[M+4],pr[M/10+1000],m=0;
unordered_map<ll,ll>mp;
ll inv(ll x,ll p){
    ll ans=1;
    for(int m=p-2;m;m>>=1){
        if(m&1) ans=ans*x%p;
        x=x*x%p;
    }
    return ans;
}
ll inv2= inv(2,mod);
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
    ans=(ans+mod)%mod;
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
    for(ll d=2; d <= N; d<<=1)
        ans= (ans + sum_phi(N / d) - 1) % mod;
    printf("%lld\n",ans);
}
```