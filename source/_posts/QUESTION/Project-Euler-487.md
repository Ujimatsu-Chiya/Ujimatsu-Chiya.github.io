---
title: Project Euler 487
category:
  - Project Euler
tags:
mathjax: true
date: 2022-07-27 23:50:34
---

<escape><!-- more --></escape>

# Project Euler 487

## 题目

### Sums of power sums

Let $f_k(n)$ be the sum of the $k^{\text{th}}$ powers of the first $n$ positive integers.

For example, $f_2(10) = 1^2 + 2^2 + 3^2 + 4^2 + 5^2 + 6^2 + 7^2 + 8^2 + 9^2 + 10^2 = 385.$

Let $S_k(n)$ be the sum of $f_k(i)$ for $1 \le i \le n$. For example, $S_4(100) = 35375333830.$

What is $\sum (S_{10000}(10^{12}) \bmod p)$ over all primes $p$ between $2\cdot 10^9$ and $2\cdot10^9 + 2000$?

## 解决方案

注意到：

$$\begin{aligned}
S_k(n)&=\sum_{i=1}^n\sum_{j=1}^i j^k=\sum_{i=1}^n (n-i+1)\cdot i^k=(n+1)\cdot\sum_{i=1}^n i^k-\sum_{i=1}^n i^{k+1}\\
&=(n+1) f_k(n)-f_{k+1}(n)
\end{aligned}$$

那么现在问题就转变成了求$f_k(n)$。

[Faulhaber公式](https://en.wikipedia.org/wiki/Faulhaber%27s_formula)直接导出了$f_k(n)$：

$$f_k(n)=\sum_{i=1}^n i^k=\dfrac{n^{k+1}}{k+1}+\dfrac{1}{2}n^k+\sum_{i=2}^{k} \dfrac{B_i}{i!}\cdot\dfrac{k!}{(k-i+1)!}\cdot n^{k-i+1}$$

其中$B_i$是第$i$个[伯努利数](https://en.wikipedia.org/wiki/Bernoulli_number)。在这个页面中伯努利数一共有两个版本，不过无论采用哪个版本都不会影响到上式的结果。以$B_n^{+}$为例，那么[这里](https://en.wikipedia.org/wiki/Bernoulli_number#Recursive_definition)给出了$B_n^{+}$的递推式：

$$B_n^{+}=
\left \{\begin{aligned}
  &1 & & \text{if}\quad n=0 \\
  &1-\sum_{k=0}^{n-1} B_k^{+}\cdot \dfrac{n!}{k!(n-k+1)!}& & \text{else}
\end{aligned}\right.
$$

可以发现，当$n>1$并且$n$为奇数时，$B_n=0$。实现时可以通过这个规律进行加速。

那么如果直接按照上面的公式计算$f_k(n)$的值，一次计算需要花费$O(k^2)$的时间复杂度。在题目中的区间中一共有$100$个质数，直接代入公式进行计算效率将会比较低。

可以证明，当$p-1\nmid k$时，$\sum_{i=1}^p i^k \equiv 0\pmod p.$

原因：令$g$为乘法群$\mathbb{Z}_p^{\star}$上的原根，那么原式就可以写成：

$$\sum_{i=1}^p (g^{i})^k \equiv \sum_{i=1}^p (g^k)^i\equiv g^k\cdot\dfrac{(g^k)^{p-1}-1}{g^k-1}\equiv 0\pmod p$$

由于$p-1\nmid k$，因此$g^k\neq 1$。后面的式子通过费马小定理即可知道其值为$0$。

因此，有

$$f_k(n)\equiv f_k(n\%p)\equiv \sum_{i=1}^{p-1-n\%p} (-i)^k\equiv (-1)^k\cdot f_k(p-1-n\%p)\pmod p$$

在这道题中，$p-1-n\%p$是一个很小的数。当$p$接近$ 2\cdot 10^9+2000$时，$p-1-n\%p$也不到$10^7$。因此可以通过暴力计算$f_k(p-1-n\%p)\pmod p$的值。

## 代码

```C++
# include <bits/stdc++.h>
# include "tools.h"
using namespace std;
typedef long long ll;
const int K=10000;
const ll N=1e12;
const int L=2000000000,R=2000002000;
ll B[K+6];
ll fac[K+6],inv[K+6],finv[K+6];
ll cal(ll k,ll p){
    ll n=N%p;
    ll pwn=n,ans=0;
    for(int i=k;i>=2;i--){
        ans=(ans+B[i]*finv[i]%p*fac[k]%p*finv[k-i+1]%p*pwn%p)%p;
        pwn=pwn*n%p;
    }
    return (ans+pwn*inv[2]%p+pwn*n%p*inv[k+1])%p;
}
ll solve(ll p){
    fac[0]=fac[1]=inv[1]=finv[0]=finv[1]=1;
    for(int i=2;i<=K+3;i++){
        fac[i]=fac[i-1]*i%p;
        inv[i]=(p-p/i)*inv[p%i]%p;
        finv[i]=finv[i-1]*inv[i]%p;
    }
    B[0]=1;
    B[1]=inv[2];
    for(int m=2;m<=K+3;m+=2){
        if(m&1) continue;
        B[m]=(p+p+1-inv[m+1]-inv[2])%p;
        for(int k=2;k<m;k+=2)
            B[m]=(B[m]-fac[m]*finv[m-k+1]%p*finv[k]%p*B[k]%p+p)%p;
    }
    ll n=N%p;
    ll ans=((n+1)*cal(K,p)-cal(K+1,p)+p)%p;
    return ans;
}
int main(){
    ll ans=0;
    for(int i=L;i<=R;i++)
        if(is_prime(i)) ans+=solve(i);
    printf("%lld\n",ans);
}

```

```C++
# include <bits/stdc++.h>
# include "tools.h"
using namespace std;
typedef long long ll;
const int K=10000;
const ll N=1e12;
const int L=2000000000,R=2000002000;
ll qpow(ll n,ll m,ll mod){
    ll a=1;
    for(;m;m>>=1){
        if(m&1) a=a*n%mod;
        n=n*n%mod;
    }
    return a;
}
ll solve(ll p){
    ll n=N%p;
    ll b=p-1-n;
    ll t1=0,t2=0;
    for(int i=1;i<=b;i++){
        ll x=qpow(i,K,p);
        t1=(t1+x)%p;
        t2=(t2+x*i)%p;
    }
    ll ans=K&1?t1*(n+1)+t2:-t1*(n+1)-t2;
    return (ans%p+p)%p;

}
int main(){
    ll ans=0;
    for(int i=L;i<=R;i++)
        if(is_prime(i)) ans+=solve(i);
    printf("%lld\n",ans);
}

```
