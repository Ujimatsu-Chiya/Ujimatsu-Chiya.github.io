---
title: Project Euler 668
category:
  - Project Euler
tags:
mathjax: true
date: 2022-07-27 23:49:52
---

<escape><!-- more --></escape>

# Project Euler 668

## 题目

### Square root smooth Numbers

A positive integer is called *square root smooth* if all of its prime factors are strictly less than its square root.

Including the number $1$, there are $29$ square root smooth numbers not exceeding $100$.

How many square root smooth numbers are there not exceeding $10\,000\,000\,000$?

## 解决方案

令$N=10^{10}$。我们考虑这个问题的对立：$N$以内有多少个数$n$，满足其最大的质因数$p$大于等于$n$的平方根？也就是说，$p\ge\lfloor\dfrac{n}{p}\rfloor$。

假设质数集合为$P$。那么，考虑以每个质数$p$作为这个最大质因数，分开计算。那么，数$p,2p,3p,\dots,(p-1)p,p^2$都是满足要求的数。

因此，题目的答案为

$$N-\sum_{p\in P} \min(p,\lfloor\dfrac{N}{p}\rfloor)=N-\sum_{p\in P,p\le \sqrt{N}}p-\sum_{p\in P,p> \sqrt{N}} \lfloor\dfrac{N}{p}\rfloor$$

对于式子的第二块，直接枚举$\sqrt{N}$以内的质数并相加即可。

对于式子的第三块，可以写成：

$$\sum_{p\in P,p> \sqrt{N}} \lfloor\dfrac{N}{p}\rfloor=\sum_{i=2}^{\lfloor\sqrt{N}\rfloor}(\pi(\dfrac{N}{i-1})-\pi(\dfrac{N}{i}))\cdot(i-1)$$

其中，$\pi(n)$是质数计数函数，即$n$以内的质数个数。这条式子说明，有$\pi(\dfrac{N}{i-1})-\pi(\dfrac{N}{i})$个质数$p$，满足$1\sim N$中有$i-1$个数是$p$的倍数，它们的贡献为$(i-1)$。

计算函数$\pi$考虑使用[Lehmer公式](https://mathworld.wolfram.com/LehmersFormula.html)帮助计算。

## 代码

```C++
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const ll N = 10000000000;
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
int main() {
    clock_t cl = clock();
    for (ll i = 2; i <= M; i++) {
        if (!vis[i]) {
            for (ll j = i * i; j <= M; j += i) vis[j] = 1;
            pr[++m] = i;
        }
        sum[i] = m;
    }
    ll ans=0;
    for(int i=1;i<=m&&1ll*pr[i]*pr[i]<=N;i++)
        ans+=pr[i];
    for(ll i=2;i*i<=N;i++)
        ans+=(pi(N/(i-1))-pi(N/i))*(i-1);
    ans=N-ans;
    printf("%lld\n",ans);
}

```
