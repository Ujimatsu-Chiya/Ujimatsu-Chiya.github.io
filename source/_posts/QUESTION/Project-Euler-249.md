---
title: Project Euler 249
category:
  - Project Euler
tags:
  - 动态规划
mathjax: true
date: 2022-05-30 20:28:31
---

<escape><!-- more --></escape>

# Project Euler 249

## 题目

### Prime Subset Sums

Let $S = \{2, 3, 5, \dots, 4999\}$ be the set of prime numbers less than $5000$.

Find the number of subsets of $S$, the sum of whose elements is a prime number.

Enter the rightmost $16$ digits as your answer.

## 解决方案

我们使用动态规划的思想解决集合的计数问题。

令$N=5000,M$为小于$N$的质数个数。

通过筛法找出质数后，存放在数组$pr$中。令$f(i,j)(0\le i\le M,0\le j\le \sum_{k=1}^i pr[k])$为前$i$个质数组成的集合中，有多少个和为$j$的子集。不难列出如下状态转移方程：

$$
f(i,j)=
\left \{\begin{aligned}
  &1  & & \mathrm{if\quad} i=0\&j=0 \\
  &f(i-1,j) & & \mathrm{else if\quad} j<pr[i] \\
  &f(i-1,j)+f(i-1,j-pr[i]) & & \mathrm{else}
\end{aligned}\right.
$$

这是一个较为典型的01背包问题，对于方程最后一行，$pr[i]$要么被使用了，将所有$f(i-1,j-pr[i])$的所有方案都添加一个$pr[i]$；要么没被使用，直接从上一次的状态$f(i-1,j)$直接记录。

最终答案只需要计算$\sum_{j}f(M,j)$，其中$j$是质数。

## 代码

```C++
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N=5000;
ll mod=1e16;
const int M = N * N / log2(N)+24;
bool b[M];
int pr[M],m=0;
ll f[M];
void sieve(int n) {
    memset(b, 0, sizeof(b));
    m = 0;
    for (int i = 2; i <= n; i++) {
        if (b[i]) continue;
        pr[++m] = i;
        for (int j = i + i; j <= n; j += i)
            b[j] = 1;
    }
}
int main() {
    sieve(N - 1);
    int sum = 0;
    f[0] = 1;
    for (int i = 1; i <= m; i++) {
        int p = pr[i];
        sum += p;
        for (int j = sum; j >= p; j--) {
            f[j] += f[j - p];
            if (f[j] >= mod) f[j] -= mod;
        }
    }
    sieve(sum);
    ll ans = 0;
    for (int i = 1; i <= m; i++)
        ans = (ans + f[pr[i]]) % mod;
    printf("%lld\n", ans);
}
```
