---
title: Project Euler 712
tags:
  - Project Euler
mathjax: true
date: 2022-07-27 23:50:22
---

<escape><!-- more --></escape>

# Project Euler 712

## 题目

### Exponent Difference

For any integer $n>0$ and prime number $p,$ define $\nu_p(n)$ as the greatest integer $r$ such that $p^r$ divides $n$.

Define $$D(n, m)  = \sum_{p \text{ prime}} \left| \nu_p(n) - \nu_p(m)\right|.$$ For example, $D(14,24) = 4$.

Furthermore, define $$S(N) = \sum_{1 \le n, m \le N} D(n, m).$$ You are given $S(10) = 210$ and $S(10^2) = 37018$.

Find $S(10^{12})$. Give your answer modulo $1\,000\,000\,007$.

## Lehmer公式

[Lehmer公式](https://mathworld.wolfram.com/LehmersFormula.html)给出了质数计数函数$\pi$的一个计算方式：

$$\pi(x)=\varphi(x,a)+\dfrac{(b+a-2)(b-a+1)}{2}-\sum_{i=a+1}^b\pi(\dfrac{x}{p_i})-\sum_{i=a+1}^c\sum_{j=i}^{b_i}(\pi(\dfrac{x}{p_ip_j})-(j-1))$$

其中，$p_i$表示第$i$个质数，$a=\pi(\sqrt[4]{x}),b=\pi(\sqrt{x}),c=\pi(\sqrt[3]{x}),b_i=\pi(\sqrt{\dfrac{x}{p_i}})$
其中$\varphi(x,a)$是$n$以内的数中，质因数只由第$a+1$个及以后的质数的个数，用容斥原理可以写成：

$$\varphi(x,a)=x-\sum_{i=1}^a\lfloor\dfrac{x}{p_i}\rfloor+\sum_{1\le i\le j\le a}\lfloor\dfrac{x}{p_ip_j}\rfloor-\dots$$

为了方便计算，[页面](https://en.wikipedia.org/wiki/Meissel%E2%80%93Lehmer_algorithm#Expanding_%F0%9D%9C%91(x,_a))说明$\varphi(x,a)$还可以写成以下递推式形式：

$$
\varphi(x,a)=
\left \{\begin{aligned}
  &\lceil\dfrac{x}{2}\rceil  & & \mathrm{if\quad}x=0\vee a=1 \\
  &\varphi(x,a-1)-\varphi(\lfloor\dfrac{x}{p_a}\rfloor,a-1) & & \mathrm{else}
\end{aligned}\right.
$$

在计算函数$\pi$和$\varphi$时，需要使用记忆化方法记录函数值。

## 解决方案

本解决方案参考了Thread中的一些内容。

令$N=10^{12}$。不难想到，单独考虑每一个的质数$p$，求取它们的贡献并相加。

假设质数集合为$P$。我们考虑将$N$以内的质数分成两部分考虑：小于等于$\lfloor\sqrt{N}\rfloor$和大于$\lfloor\sqrt{N}\rfloor$的两部分。

小于等于$\lfloor\sqrt{N}\rfloor$的质数$p$这一部分贡献为：

$$\sum_{p\in P,p\le \lfloor\sqrt{N}\rfloor}\sum_{i=0}^{+\infty}\sum_{j=i+1}^{+\infty}2(\lfloor\dfrac{N}{p^i}\rfloor-\lfloor\dfrac{N}{p^{i+1}}\rfloor)(\lfloor\dfrac{N}{p^j}\rfloor-\lfloor\dfrac{N}{p^{j+1}}\rfloor)(j-i)$$

其中，上面的式子可以化简：

$$\begin{aligned}
&\sum_{i=0}^{+\infty}\sum_{j=i+1}^{+\infty}(\lfloor\dfrac{N}{p^i}\rfloor-\lfloor\dfrac{N}{p^{i+1}}\rfloor)(\lfloor\dfrac{N}{p^j}\rfloor-\lfloor\dfrac{N}{p^{j+1}}\rfloor)(j-i)\\
=&\sum_{i=0}^{+\infty}(\lfloor\dfrac{N}{p^i}\rfloor-\lfloor\dfrac{N}{p^{i+1}}\rfloor)\sum_{j=i+1}^{+\infty}(\lfloor\dfrac{N}{p^j}\rfloor-\lfloor\dfrac{N}{p^{j+1}}\rfloor)(j-i)\\
=&\sum_{i=0}^{+\infty}(\lfloor\dfrac{N}{p^i}\rfloor-\lfloor\dfrac{N}{p^{i+1}}\rfloor)\sum_{j=1}^{+\infty}(\lfloor\dfrac{N}{p^{i+j}}\rfloor-\lfloor\dfrac{N}{p^{i+j+1}}\rfloor)\cdot j\\
=&\sum_{i=0}^{+\infty}(\lfloor\dfrac{N}{p^i}\rfloor-\lfloor\dfrac{N}{p^{i+1}}\rfloor)\sum_{j=1}^{+\infty}\lfloor\dfrac{N}{p^{i+j}}\rfloor\\
=&(\sum_{i=0}^{+\infty}\lfloor\dfrac{N}{p^i}\rfloor\cdot\sum_{j=1}^{+\infty}\lfloor\dfrac{N}{p^{i+j}}\rfloor)-(\sum_{i=0}^{+\infty}\lfloor\dfrac{N}{p^{i+1}}\rfloor\cdot\sum_{j=1}^{+\infty}\lfloor\dfrac{N}{p^{i+j}}\rfloor)\\
=&N\cdot\sum_{j=1}^{+\infty}\lfloor\dfrac{N}{p^j}\rfloor+ (\sum_{i=1}^{+\infty}\lfloor\dfrac{N}{p^i}\rfloor\cdot\sum_{j=1}^{+\infty}\lfloor\dfrac{N}{p^{i+j}}\rfloor)-(\sum_{i=1}^{+\infty}\lfloor\dfrac{N}{p^{i}}\rfloor\cdot\sum_{j=1}^{+\infty}\lfloor\dfrac{N}{p^{i+j-1}}\rfloor)\\
=&N\cdot\sum_{j=1}^{+\infty}\lfloor\dfrac{N}{p^j}\rfloor+ (\sum_{i=1}^{+\infty}\lfloor\dfrac{N}{p^i}\rfloor\cdot\sum_{j=1}^{+\infty}(\lfloor\dfrac{N}{p^{i+j}}\rfloor-\lfloor\dfrac{N}{p^{i+j-1}}\rfloor))\\
=&N\cdot\sum_{j=1}^{+\infty}\lfloor\dfrac{N}{p^j}\rfloor- (\sum_{i=1}^{+\infty}\lfloor\dfrac{N}{p^i}\rfloor\cdot\lfloor\dfrac{N}{p^i}\rfloor)\\
=&\sum_{i=1}^{+\infty}(N-\lfloor\dfrac{N}{p^i}\rfloor)\cdot\lfloor\dfrac{N}{p^i}\rfloor\\
\end{aligned}$$

那么计算以下式子只需要计算$O(\sqrt{N}\cdot \log N)$的时间复杂度：

$$\sum_{p\in P,p\le \lfloor\sqrt{N}\rfloor}\sum_{i=1}^{+\infty}(N-\lfloor\dfrac{N}{p^i}\rfloor)\cdot\lfloor\dfrac{N}{p^i}\rfloor\\$$

大于$\lfloor\sqrt{N}\rfloor$的质数$p$这一部分贡献如下。注意到，$1\sim N$中，$p$的指数最多为$1$：

$$\sum_{i=2}^{\lfloor\sqrt{N}\rfloor}(\pi(\dfrac{N}{i-1})-\pi(\dfrac{N}{i}))\cdot(i-1)(N-i+1)$$

这条式子说明，有$\pi(\dfrac{N}{i-1})-\pi(\dfrac{N}{i})$个质数$p$，满足$1\sim N$中有$i-1$个数是$p$的倍数，它们的贡献为$(i-1)(N-i+1)$。

计算函数$\pi$考虑使用Lehmer公式帮助计算。

## 代码

本代码效率略低，约$30s$，仍有很大改进空间。

```C++
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const ll N = 1000000000000;
ll mod=1000000007;
const ll M = N<=10000?10000:pow(N, 2.0 / 3) + 2;
bool vis[M + 1];
int sum[M + 1],pr[M + 1],m;
unordered_map<ll,ll> mp,mq;
ll phi(ll x, ll a) {
    if (a == 1 || x == 0)return (x + 1) / 2;
    ll &v = mp[(x << 10) + a];
    if (v)return v;
    return v = phi(x, a - 1) - phi(x / pr[a], a - 1);
}
ll pi(ll n) {
    if (n <= M)return sum[n];
    ll &v = mq[n];
    if (v) return v;
    ll a = pi(pow(n, 1.0 / 4));
    ll b = pi(sqrt(n));
    ll c = pi(pow(n, 1.0 / 3));
    ll s = phi(n, a) + (b + a - 2) * (b - a + 1) / 2;
    for (ll i = a + 1; i <= b; i++) {
        ll w = n / pr[i];
        s -= pi(w);
        ll bi = pi(sqrt(w));
        if (i <= c) {
            for (ll j = i; j <= bi; j++)
                s += j - 1 - pi(w / pr[j]);
        }
    }
    return v = s;
}
ll cal(ll p){
    ll ans=0;
    for(ll x=N/p;x;x/=p){
        ans=(ans+x%mod*((N-x)%mod))%mod;
    }
    return ans*2%mod;
}
int main() {
    for (ll i = 2; i <= M; i++) {
        if (!vis[i]) {
            for (ll j = i * i; j <= M; j += i) vis[j] = 1;
            pr[++m] = i;
        }
        sum[i] = m;
    }
    ll ans=0;
    for(int i=1;i<=m&&1ll*pr[i]*pr[i]<=N;i++)
        ans=(ans+cal(pr[i]))%mod;
    for(int i=2;1ll*i*i<=N;i++)
        ans=(ans+(N-i+1)%mod*(i-1)%mod*((pi(N/(i-1))-pi(N/i))%mod)*2%mod)%mod;
    printf("%lld\n",ans);
}

```
