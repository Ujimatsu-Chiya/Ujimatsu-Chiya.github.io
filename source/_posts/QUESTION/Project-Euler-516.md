---
title: Project Euler 516
category:
  - Project Euler
tags:
mathjax: true
date: 2022-06-13 21:21:23
---

<escape><!-- more --></escape>

# Project Euler 516

## 题目

### $5$-smooth totients

$5$-smooth numbers are numbers whose largest prime factor doesn’t exceed $5$.

$5$-smooth numbers are also called Hamming numbers.

Let $S(L)$ be the sum of the numbers $n$ not exceeding $L$ such that Euler’s totient function $\varphi(n)$ is a Hamming number.

$S(100)=3728$.

Find $S(10^{12})$. Give your answer modulo $2^{32}$.

## 解决方案

可以发现，这些数都是形如以下形式：

$$2^a3^b5^c\cdot p_1p_2p_3\dots$$

其中$p_i$是一些质数，它们满足$p_i-1=2^x3^y5^z$。这些质数引入的欧拉函数的质因子只有$2,3,5$。

那么，枚举的过程分为两部分：一部分是枚举出$2^a3^b5^c$的值，直接暴力循环枚举。另一部分是枚举右边大于$5$的质数的乘积，通过递归进行枚举。

最终，这两部分数两两之间的乘积就是答案。

## 代码

```C++
#include <bits/stdc++.h>
typedef long long ll;
using namespace std;
const ll N = 1000000000000;
const ll M = sqrt(N)+4;
ll mod = 1ll<<32;
bool vis[M+4];
vector<ll> pr,a,p;
bool is_prime(ll w) {
    for (ll x: pr) {
        if (x * x > w) break;
        if (w % x == 0) return false;
    }
    return true;
}
ll ans=0;
void dfs(int f,ll w) {
    for (ll x: a) {
        ll z = w * x;
        if (z > N) break;
        ans = (ans + z) % mod;
    }
    for (; f < p.size() && p[f] <= N / w; f++) {
        dfs(f + 1, w * p[f]);
    }
}
int main() {
    for (ll i = 2; i <= M; i++) {
        if (vis[i]) continue;
        for (ll j = i * i; j <= M; j += i)
            vis[j] = 1;
        pr.push_back(i);
    }
    for (ll x = 1; x <= N; x *= 2)
        for (ll y = x; y <= N; y *= 3)
            for (ll z = y; z <= N; z *= 5) {
                a.push_back(z);
                if (z + 1 > 5 && is_prime(z + 1)) p.push_back(z + 1);
            }
    sort(a.begin(), a.end());
    sort(p.begin(), p.end());
    dfs(0, 1);
    printf("%lld\n", ans);
}
```
