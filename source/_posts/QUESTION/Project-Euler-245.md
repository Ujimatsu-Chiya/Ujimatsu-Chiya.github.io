---
title: Project Euler 245
category:
  - Project Euler
tags:
  - OEIS
mathjax: true
date: 2022-06-18 21:59:07
---

<escape><!-- more --></escape>

# Project Euler 245

## 题目

### Coresilience

We shall call a fraction that cannot be cancelled down a resilient fraction.

Furthermore we shall define the resilience of a denominator, $R(d)$, to be the ratio of its proper fractions that are resilient; for example, $R(12) = \dfrac{4}{11}$.

The resilience of a number $d \gt 1$ is then $\dfrac{\varphi(d)}{d - 1}$, where $\varphi$ is Euler's totient function.

We further define the **coresilience** of a number $n \gt 1$ as $C(n) = \dfrac{n - \varphi(n)}{n - 1}$.

The coresilience of a prime $p$ is $C(p) = \dfrac{1}{p - 1}$.

Find the sum of all <b>composite</b> integers $1 \lt n \le 2 \times 10^{11}$, for which $C(n)$ is a <dfn title="A fraction with numerator 1">unit fraction</dfn>.

## 解决方案

令$N=2\times 10^{11}$。

证明：如果$C(n)$是一个单位分数，那么$n$是一个无平方因子数。

假设$p$是$n$的任意一个质因子，$e$是一个最大的正整数使得$p^e|n$。

如果$C(n)$是一个单位分数，那么可以写成存在一个整数$m$，满足$m=\dfrac{n-1}{n-\varphi(n)}$

那么，$\varphi(n)$中有一个因子$p^{e-1}$。同时不难发现$p^{e-1}|n$。因此如果$m$是一个整数，那么$p^{e-1}|1$，从而得出$e=1$。

因此，$n$是一个无平方因子数。

证明：$n$是奇数。也就是说，$n$没有$2$的质因子。

如果$n$是偶数，那么$n-1$是奇数，$n-\varphi(n)$是偶数，偶数不可能整除一个奇数，因此$n$不可能是偶数。

证明：$m$是偶数。

由于$n$是奇数$n-1$是偶数，$\varphi(n)$是偶数，因此$m$一定是一个偶数。

假设$n=p_1p_2\dots p_k$，并且对于$1< i\le k$，都有$p_{i-1}< p_i$。

考虑当前已经有$x=\prod_{i=1}^{k-1}p_i,y=\prod_{i=1}^{k-1}(p_i-1)$，现在枚举一个新的$p=p_k$，有$n=xp$。

那么，$\dfrac{xp-1}{xp-y(p-1)}=\dfrac{xp-1}{(x-y)p+y}=m$

容易发现，随着$p$值增长，$m$也增长（由反比例函数的性质可知）。但是，$m$的增长速度非常慢（因为分母中有个$x-y$，并且$x-y$的值一般是比较接近$x$的）。可以求出$m$的范围，再通过枚举$m$反推出$p$。

那么，根据以上约束，不难得出$p_{k-1}< p\le\dfrac{N}{x}$

因此，可以给出$\dfrac{xp_{k-1}}{(x-y)p_{k-1}+y}< m\le\dfrac{N-1}{N-y(\frac{N}{x})+y}$

只需要枚举这个区间中所有的偶数$m$即可，这个区间范围比较小。根据$m$，重新计算出$p=\dfrac{1+mx}{x-mx+my}$，并判断$p$是否为一个整数并且为一个质数。如果$p$满足要求，那么说明找到了一个答案$np$。

另外一个问题：$x$的枚举。$x$的枚举比较容易，只需要枚举所有的质数之积即可。但是，用$x$扩展到下一个$x'=xq$时，需要保证$q\le \sqrt{\dfrac{N}{x}}$，因为$q$并非是答案中最大的质因数。

另外，前几项在OEIS中查询后，结果为[A160599](https://oeis.org/A160599)。

## 代码

```C++
#include<bits/stdc++.h>
#include "tools.h"
typedef long long ll;
using namespace std;
const ll N = 200000000000;
const int M = sqrt(N)+4;
int pr[M/10+1000],m=0;
bool vis[M+4];
ll ans=0;
void dfs(int f, ll x, ll y) {
    ll p_max = int_sqrt(N / x);
    for (int i = f + 1; i <= m && pr[i] <= p_max; i++) {
        dfs(i, x * pr[i], y * (pr[i] - 1));
    }
    ll p = f < m ? pr[f + 1] : pr[f] + 2;
    ll num = p * x - 1, den = p * (x - y) + y;
    ll kl = (num + den - 1) / den;
    if (kl % 2 == 1) kl += 1;
    num = (N / x) * x - 1;
    den = (N / x) * (x - y) + y;
    ll kr = num / den;
    for (ll k = kl; k <= kr; k += 2) {
        num = k * y + 1;
        den = x - k * (x - y);
        if (num % den == 0) {
            ll p = num / den;
            if (is_prime(p))
                ans += x * p;
        }
    }
}

int main() {
    for (int i = 2; i <= M; i++) {
        if (vis[i]) continue;
        pr[++m] = i;
        for (ll j = 1ll * i * i; j <= M; j += i)
            vis[j] = 1;
    }
    for (int i = 2; i <= m; i++)
        dfs(i, pr[i], pr[i] - 1);
    printf("%lld\n", ans);
}
```
