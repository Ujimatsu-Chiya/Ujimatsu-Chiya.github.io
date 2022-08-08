---
title: Project Euler 274
date: 2022-04-09 11:31:03
category:
  - Project Euler
tags:
mathjax: true
---
<escape><!-- more --></escape>

# Project Euler 274

## 题目

### A lagged Fibonacci sequence

For each integer $p > 1$ coprime to $10$ there is a *positive divisibility multiplier* $m < p$ which preserves divisibility by $p$ for the following function on any positive integer, $n$:

$f(n) = (\mathrm {all\ but\ the\ last\ digit\ of\ }n) + (\mathrm{the\ last\ digit\ of\ }n) * m$

That is, if $m$ is the divisibility multiplier for $p$, then $f(n)$ is divisible by $p$ if and only if $n$ is divisible by $p$.

(When $n$ is much larger than $p$, $f(n)$ will be less than $n$ and repeated application of f provides a multiplicative divisibility test for $p$.)

For example, the divisibility multiplier for $113$ is $34$.

$f(76275) = 7627 + 5 * 34 = 7797$ : $76275$ and $7797$ are both divisible by $113$

$f(12345) = 1234 + 5 * 34 = 1404$ : $12345$ and $1404$ are both not divisible by $113$

The sum of the divisibility multipliers for the primes that are coprime to $10$ and less than $1000$ is $39517$.

What is the sum of the divisibility multipliers for the primes that are coprime to $10$ and less than $10^7$?

## 解决方案

原题等价为：
对于$\forall a \in \mathbb{Z},b\in [0,9] \cap \mathbb{Z}$，有

$$10a+b \equiv 0 (\mod p) \Leftrightarrow a+mb\equiv 0(\mod p)$$

即为$10a+10mb\equiv 0 (\mod p)$

当上述条件满足时，有：

$10a\equiv -b \equiv -10 mb(\mod p)$

由此得$10mb-b\equiv 0(\mod p)$。

即为$(10m-1)b\equiv 0(\mod p)$，对于所有$b$成立。

令$b=1$，那么$m$满足$10m\equiv 1 (\mod p)$。直接计算$10$对质数$p$的逆元即可。

## 代码

```C++
# include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N = 1e7;
int pr[N + 4], v[N + 4], p = 0;
ll qpow(ll n, ll m, ll mod) {
    ll a = 1;
    for (; m; m >>= 1) {
        if (m & 1) a = a * n % mod;
        n = n * n % mod;
    }
    return a;
}
int main() {
    for (int i = 2; i < N; i++) {
        if (v[i] == 0) {
            pr[++p] = i;
            v[i] = i;
        }
        for (int j = 1; j <= p; j++) {
            if (pr[j] > v[i] || pr[j] > N / i) break;
            v[i * pr[j]] = pr[j];
        }
    }
    ll ans = qpow(10, 3 - 2, 3);
    for (int i = 4; i <= p; i++)
        ans += qpow(10, pr[i] - 2, pr[i]);
    printf("%lld\n", ans);
}
```
