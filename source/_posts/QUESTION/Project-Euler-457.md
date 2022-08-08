---
title: Project Euler 457
category:
  - Project Euler
tags:
mathjax: true
date: 2022-08-05 21:41:26
---

<escape><!-- more --></escape>

# Project Euler 457

## 题目

### A polynomial modulo the square of a prime

Let $f(n) = n^2 - 3n - 1$.

Let $p$ be a prime.

Let $R(p)$ be the smallest positive integer $n$ such that $f(n) \mod p^2 = 0$ if such an integer $n$ exists, otherwise $R(p) = 0$.

Let $SR(L)$ be $\sum R(p)$ for all primes not exceeding $L$.

Find $SR(10^7)$.

## Tonelli–Shanks算法

[Tonelli–Shanks算法](https://en.wikipedia.org/wiki/Tonelli%E2%80%93Shanks_algorithm)是用于求解方程$x^2\equiv a(\mod p)$的一个算法，其中$p$是一个质数。

为求解这个方程，第一步首先需要使用[欧拉准则](https://en.wikipedia.org/wiki/Euler%27s_criterion)进行判断方程是否有解：

如果有解（$a$是二次剩余），那么有$a^{\frac{p-1}{2}}\equiv 1(\mod p)$；否则（$a$不是二次剩余），有$a^{\frac{p-1}{2}}\equiv -1(\mod p)$。

如果$p\% 4=3$，那么方程的其中一个解为$a^{\frac{p+1}{4}}\%P$。

否则，先将$p-1$写成$p-1=Q2^S$，其中$Q$是一个奇数。并且随机找到一个$z$使得$z$是$p$的一个非二次剩余（注意这样的$z$有一半数量，很容易找到）。

接下来初始化这一系列值：

$\begin{aligned}
m&\leftarrow S\\
c&\leftarrow z^Q\\
t&\leftarrow a^Q\\
r&\leftarrow a^{\frac{Q+1}{2}}
\end{aligned}$

然后对以下过程进行无限循环：

- 如果$t=0$，返回$x=0$。
- 如果$t=1$，返回$x=r$。
- 找到最小的$i$使得$t^{2^i}\equiv 1(\mod p)$
- 接下来继续进行一系列赋值：

$\begin{aligned}
b&\leftarrow c^{2^{m-i-1}}\\
m&\leftarrow i\\
c&\leftarrow b^2\\
t&\leftarrow tb^2\\
r&\leftarrow rb
\end{aligned}$

整个算法的期望时间复杂度为$O(\log^2 p)$。

## Hensel引理

[Hensel引理](https://en.wikipedia.org/wiki/Hensel%27s_lemma#Hensel_lifting)通常用于求解方程$f(x)\equiv 0(\mod p^k)$，其中$f(x)$是一个整系数多项式，$p$是一个质数。它的基本思想是假设已知方程$f(x)\equiv 0(\mod p^{k-1})$的根，再将它扩展到$f(x)\equiv 0(\mod p^k)$时的情况。

假设整数$r$满足$f(r)\equiv0(\mod p^{k-1})$，那么考虑关于未知数$t$的方程：

$$f(r+tp^{k-1})\equiv 0(\mod p^k)\qquad(1)$$

1. 如果$f'(r)\not\equiv 0(\mod p)$，那么存在唯一的正整数$t$使得$(1)$成立。这个$t$满足

$$\displaystyle tf'(r)\equiv -\dfrac{f(r)}{p^{k-1}}{\pmod {p}}$$

2. 如果$f'(r)\equiv 0(\mod p),f(r)\equiv0(\mod p)$，那么对于任意$t$，方程$(1)$恒成立。
3. 如果$f'(r)\equiv 0(\mod p),f(r)\not\equiv0(\mod p)$，那么方程$(1)$无解。

## 解决方案

题目的目标为求解方程$n^2-3n-1\equiv 0(\mod p^2)$。

由于$p$是一个质数（$p=2$时容易发现无解，不讨论），那么方程两边乘以一个$4$，配方后得到：

$$(2n-3)^2\equiv13(\mod p^2)$$

为了避免特殊判断，当质数$p\le 13$时，$R(p)$将会被暴力计算出来。

令$x=2n-3$，那么原方程的解将通过$n=\dfrac{x+3}{2}$计算出来。

令$f(x)=x^2-13$，假设通过Tonelli–Shanks算法求解得出方程$f(x)\equiv0(\mod p)$的值为$r$。

为求解$f(x)\equiv0(\mod p^2)$，根据Hensel引理，新解为$x=r+tp$，其中$t\equiv \dfrac{13-r^2}{p}\cdot (2r)^{-1}(\mod p)$

最终分别计算出两个$x$后，回代出两个$n$的值，取最小值即可。

## 代码

```C++
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;

const int M=10000000;
int v[M+4],pr[M/10+1000],m=0;
ll qpow(ll n,ll m,ll p){
    ll a=1;
    for(;m;m>>=1){
        if(m&1) a=a*n%p;
        n=n*n%p;
    }
    return a;
}
int shanks(int a,int p) {
    if (p % 4 == 3)
        return qpow(a, (p + 1) / 4, p);
    int Q = p - 1;
    int S = 0;
    for (; !(Q & 1); Q >>= 1) S++;
    int z;
    for (int i = 1; i <= m; i++) {
        z = pr[i];
        if (qpow(z, (p - 1) / 2, p) == p - 1) break;
    }
    ll m = S;
    ll c = qpow(z, Q, p);
    ll t = qpow(a, Q, p);
    ll r = qpow(a, (Q + 1) / 2, p);
    while (true) {
        if (t == 0) return 0;
        if (t == 1) return r;
        ll tmp = t;
        int i;
        for (i = 0; i < m && tmp != 1; i++)
            tmp = tmp * tmp % p;
        ll b = qpow(c, 1 << (m - i - 1), p);
        m = i;
        c = b * b % p;
        t = t * c % p;
        r = r * b % p;
    }
}
int main(){
    for(int i=2;i<=M;i++){
        if(v[i]==0){
            v[i]=i;pr[++m]=i;
        }
        for(int j=1;j<=m;j++){
            if(pr[j]>v[i]||pr[j]>M/i) break;
            v[i*pr[j]]=pr[j];
        }
    }
    ll ans=0;
    for(int i=1;i<=m;i++){
        int p=pr[i];
        if(p<=13){
            for(int n=1;n<p*p;n++){
                if((n*n-3*n-1)%(p*p)==0){
                    ans+=n;
                    break;
                }
            }
        }
        else{
            if(qpow(13,(p-1)>>1,p)!=1) continue;
            ll p2=1ll*p*p;
            ll r=shanks(13,p);
            ll t=((13ll-r*r)/p*qpow(r*2,p-2,p)%p+p)%p;
            ll x=p*t+r;
            ll n=(x&1?(x+3)>>1:(x+3+p2)>>1);
            x=p2-x;
            ll m=(x&1?(x+3)>>1:(x+3+p2)>>1);
            ans+=min(n,m);
        }
    }
    printf("%lld\n",ans);
}

```
