---
title: Project Euler 501
tags:
  - Project Euler
mathjax: true
date: 2022-07-13 22:57:37
---

<escape><!-- more --></escape>

# Project Euler 501

## 题目

### Eight Divisors

The eight divisors of $24$ are $1, 2, 3, 4, 6, 8, 12$ and $24$.

The ten numbers not exceeding $100$ having exactly eight divisors are $24, 30, 40, 42, 54, 56, 66, 70, 78$ and $88$.

Let $f(n)$ be the count of numbers not exceeding $n$ with exactly eight divisors.

You are given $f(100)=10, f(1000)=180$ and $f(10^6)=224427$.

Find $f(10^{12})$.

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

令$N=10^{12}$，有$8$个因子的数分别有以下三种（以下使用的$p_i$均为质数）：

1. $p_1$
2. $p_1^3p_2$，其中满足$p_1\neq p_2$
3. $p_1p_2p_3$，其中满足$p_1<p_2<p_3$

那么不难写出三种数对应的个数为：

1. $f_1(n)=\pi(\sqrt[7]{N})$
2. $f_2(n)=\sum_{p_1\le \sqrt[3]{N}}(\pi(\dfrac{N}{p_1^3}))-\pi(\sqrt[4]{N})$
3. $f_3(n)=\sum_{p_1\le \sqrt[3]{N}}\sum_{p_1<p_2<\sqrt{\frac{N}{p_1}}}(\pi(\dfrac{N}{p_1\cdot p_2})-\pi(p_2))$

最终得到$f(n)=f_1(n)+f_2(n)+f_3(n).$

那么现在问题就转化成了使用Lehmer公式计算函数$\pi.$

## 代码

```C++
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const ll N = 1000000000000;
const ll M = pow(N, 2.0 / 3) + 2;
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
    for (ll i = 2; i <= M; i++) {
        if (!vis[i]) {
            for (ll j = i * i; j <= M; j += i) vis[j] = 1;
            pr[++m] = i;
        }
        sum[i] = m;
    }
    ll ans=0;
    ans+= pi(pow(N, 1.0 / 7));
    ll tmp;
    for (int i = 1; i <= m && (tmp = N / (1ll * pr[i] * pr[i] * pr[i])) >= 2; i++)
        ans += pi(tmp);
    ans-= pi(pow(N, 1.0 / 4));
    for (ll i = 1; 1ll * pr[i] * pr[i] * pr[i] <= N; i++)
        for (ll j = i + 1; j <= m && pr[j + 1] <= (tmp = N / (1ll * pr[i] * pr[j])); j++)
            ans += pi(tmp) - pi(pr[j]);
    printf("%lld\n", ans);
}

```
