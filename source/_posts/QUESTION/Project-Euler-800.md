---
title: Project Euler 800
tags:
  - Project Euler
  - 双指针
mathjax: true
date: 2022-05-30 20:27:53
---

<escape><!-- more --></escape>

# Project Euler 249

## 题目

### Hybrid Integers

An integer of the form $p^q q^p$ with prime numbers $p \neq q$ is called a *hybrid-integer*.

For example, $800 = 2^5 5^2$ is a hybrid-integer.

We define $C(n)$ to be the number of hybrid-integers less than or equal to $n$.

You are given $C(800) = 2$ and $C(800^{800}) = 10790$

Find $C(800800^{800800})$

## 解决方案

由于题目中仅涉及求幂，乘法等运算，可以考虑取对数进行计算，避免大整数。

令$N=P^E$，其中$P=E=800800$。不失一般性，假设$p< q$，那么写成对数形式，就是求所有有多少质数对$(p,q)$满足：

$$p\log_2q +q\log_2p\le E\log_2P$$

$q$的最大值最多能取到多少？当$p=2$时，忽略掉第一项$p\log_2q$，可以估计$q$取得的上限为$E\log_2P$。

令$M=\lceil E\log_2P\rceil$，使用线性筛枚举出$M$以内的质数，存放在数组$pr$中。

使用双指针法，在第一层循环从左到右枚举左指针$l$，第二层循环右往左枚举右指针$r$，并枚举到第一个$pr[l] \cdot \log_2pr[r]+pr[r]\cdot \log_2pr[l]< E\log_2P$的最大$r$。那么，$r$左边和$l$右边的所有质数都可以和$pr[l]$组成答案，统计这一段数的数量。

为避免log2函数使用次数过多降低效率，实现时先将所有对数值先计算出来。

## 代码

```C++
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const int P = 800800,E = 800800;
const int M = log2(P) * E + 4;
const double max_lg = log2(P) * E;
int pr[M/4+104],m=0;
int v[M];
double lg[M/4+104];
int main() {
    for (int i = 2; i <= M; i++) {
        if (v[i] == 0) {
            v[i] = i;
            pr[++m] = i;
            lg[m] = log2(pr[m]);
        }
        for (int j = 1; j <= m; j++) {
            if (pr[j] > v[i] || pr[j] > M / i) break;
            v[i * pr[j]] = pr[j];
        }
    }
    ll ans = 0;
    for (int l = 1, r = m; l <= m; l++) {
        for (; r > l && lg[l] * pr[r] + lg[r] * pr[l] > max_lg; r--);
        if (l == r) break;
        ans += r - l;
    }
    printf("%lld\n", ans);
}
```
