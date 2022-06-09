---
title: Project Euler 204
tags:
  - Project Euler
mathjax: true
date: 2022-05-30 20:28:09
---

<escape><!-- more --></escape>

# Project Euler 204

## 题目

### Generalised Hamming Numbers

A Hamming number is a positive number which has no prime factor larger than 5.

So the first few Hamming numbers are $1, 2, 3, 4, 5, 6, 8, 9, 10, 12, 15$.

There are $1105$ Hamming numbers not exceeding $10^8$.

We will call a positive number a generalised Hamming number of type $n$, if it has no prime factor larger than $n$.

Hence the Hamming numbers are the generalised Hamming numbers of type $5$.

How many generalised Hamming numbers of type $100$ are there which don't exceed $10^9$?

## 解决方案

令$N=100,M=10^9$，$N$以内的质数存放在数组$pr$中，一共有$m$个。

基本思想是：先产生有小质因子的合数，再利用这些小质因子的质数产生含有大质因子的合数。

假设数组$g[i]$存放由第$1\sim i$个质因数构成的广义汉明数，那么尝试将$g[i]$中的所有数都乘以$pr[i+1]^0,pr[i+1]^1,pr[i+1]^2,\dots$，将产生的这些数存放到数组$g[i+1]$中。

枚举发现，数组$g[m]$中的广义汉明数不多。

## 代码

```C++
# include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N = 100;
const ll M = 1e9;
vector<int>a,pr;
bool vis[N+4];
int main() {
    for (int i = 2; i <= N; i++) {
        if (vis[i]) continue;
        pr.push_back(i);
        for (int j = i * i; j <= N; j += i)
            vis[j] = true;
    }
    a.push_back(1);
    for (int p: pr) {
        int m = a.size();
        for (int i = 0; i < m; i++) {
            for (ll x = 1ll * a[i] * p; x <= M; x *= p)
                a.push_back(x);
        }
    }
    int ans = a.size();
    printf("%d\n", ans);
}
```
