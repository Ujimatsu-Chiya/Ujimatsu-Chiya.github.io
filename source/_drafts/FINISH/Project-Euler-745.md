---
title: Project Euler 745
tags:
  - Project Euler
  - 容斥原理
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 745
## 题目
### Sum of Squares II



For a positive integer, $n$, define $g(n)$ to be the maximum perfect square that divides $n$.

For example, $g(18) = 9$, $g(19) = 1$.


Also define
$$\displaystyle	S(N) = \sum_{n=1}^N g(n)$$


For example, $S(10) = 24$ and $S(100) = 767$.


Find $S(10^{14})$. Give your answer modulo $1\,000\,000\,007$.





## 解决方案

可以知道，对于所有无平方因子数$n$，都有$g(nk^2)=k^2$，因为$g(nk^2)$只取决于平方因子$k^2$。

令$N=10^{14}$，那么有

$$S(N)=\sum_{i=1}^{\lfloor\sqrt{N}\rfloor} i^2\cdot f(\lfloor\dfrac{N}{i^2}\rfloor)$$

其中$f(n)$表示$n$以内的无平方因子数。

$f(n)$可以以$O(\sqrt{n})$的时间复杂度计算，在193题已经有提及。那么本题计算$S(N)$的时间复杂度为$O(\sqrt{N}\log N)$。

$O(\sqrt{N})$的做法待补。

## 代码


```C++
# include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const ll N=1e14;
const int M=sqrt(N);
int mod=1e9+7;
int pr[M/10+100],v[M+4],mu[M+4],m=0;
ll cal(ll n){
    ll ans=0;
    for(ll i=1;i*i<=n;i++)
        ans+=(n/i/i)*mu[i];
    return ans;
}
int main(){
    mu[1]=1;
    for(int i=2;i<=M;i++){
        if(v[i]==0){
            v[i]=i;mu[i]=-1;pr[++m]=i;
        }
        for(int j=1;j<=m;j++){
            if(pr[j]>v[i]||pr[j]>M/i) break;
            v[i*pr[j]]=pr[j];
            mu[i*pr[j]]=(pr[j]==v[i]?0:-mu[i]);
        }
    }
    ll ans=0;
    for(int i=1;i<=M;i++)
        ans=(ans+cal(N/i/i)%mod*i%mod*i%mod);
    ans%=mod;
    printf("%lld\n",ans);
}

```