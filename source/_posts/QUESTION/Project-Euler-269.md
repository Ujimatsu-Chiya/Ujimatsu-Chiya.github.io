---
title: Project Euler 269
category:
  - Project Euler
tags:
  - 容斥原理
  - 动态规划
mathjax: true
date: 2022-08-05 21:40:36
---

<escape><!-- more --></escape>

# Project Euler 269

## 题目

### Polynomials with at least one integer root

A root or zero of a polynomial $P(x)$ is a solution to the equation $P(x) = 0$.

Define $P_n$ as the polynomial whose coefficients are the digits of n.

For example, $P_{5703}(x) = 5x^3 + 7x^2 + 3$.
We can see that:

- $P_n(0)$ is the last digit of $n$,
- $P_n(1)$ is the sum of the digits of $n$,
- $P_n(10)$ is $n$ itself.

Define $Z(k)$ as the number of positive integers, $n$, not exceeding $k$ for which the polynomial $P_n$ has at least one integer root.

It can be verified that $Z(100 000)$ is $14696$.

What is $Z(10^{16})$?

## 解决方案

令$N=16$。不难发现，方程$P_n(x)=0$的整数根只能在范围$[-9,0]$内，因为值$P_n(-10)$的最高次数项的绝对值一定大于其余项的绝对值之和。

如果$x=0$是方程$P_n(x)=0$的解，当且仅当$n$是$10$的倍数。这类数一共有$10^{N-1}-1+1$个，注意这里其中一个答案是$10^N$。

接下来只考虑范围$[-9,-1]$内的解情况。由于$P_n(x)$的常系数项最多为$9$，而多项式$(x+1)(x+2)(x+3)(x+4)$的常数项已经达到了$24$，因此$P_n(x)$最多只有$3$个整数根。

考虑使用容斥原理，先计算出有多少个多项式的解含有$-1,-2,\dots,-9$，再秋求和，然后再计算有多少个多项式的解同时含有$(-1,-2),(-1,-3),\dots$，并一一减去，相应的计算三个解时的情况，并加上。

考虑一个$m$位**有前导**$0$数对应的多项式$p_m(x)$，它可以写成$p_m(x)=x\cdot p_{m-1}(x) + d_m$。其中$d_m$表示常数项，$0\le d_m\le 9$，注意，$d_m$也表示这个$m$位有前导$0$数的个位。那么可以写成$p_{m-1}(x)=\dfrac{p_m(x)-d_m}{x}$，进而递归寻找更小的项。

令状态$f_3(n,b_1,b_2,b_3)(0\le n< N)$表示有多少个多项式$p_{N-n-1}(x)$，满足$p_{N-n-1}(a_k)=b_k,k=1,2,3$。那么可以写出$f$的状态转移方程：

$$
f_3(n,b_1,b_2,b_3)=
\left \{\begin{aligned}
  &1 & & \mathrm{if\quad} n=N-1\wedge 0\le b_1\le 9\wedge b_1=b_2=b_2 \\
  &0 & & \mathrm{else if\quad} n=0 \\
  &\sum_{[n=0]\le d\le 9,a_k|(b_k-d),k=1,2,3} f(n+1,\dfrac{b_1-d}{a_1},\dfrac{b_2-d}{a_2},\dfrac{b_3-d}{a_3}) & & \mathrm{else}
\end{aligned}\right.
$$

其中，$[]$表示示性函数，表示$[]$里面的值是否为真，如果为真，那么值为$1$，否则值为$0$.

方程的最后一行，表示$d_m$随意从$0\sim 9$中随意选择。由于我们一开始已经计算了个位为$0$的情况，因此个位不能选择$0$。

一开始，$p_{N-1}(x)=0$，因此同时具有$a_1,a_2,a_3$三个根的多项式个数为$f_3(0,0,0,0)$。

$f_2,f_1$的计算过程也类似。

最终用容斥原理将它们整合在一起即可。实际上，$|b_1|,|b_2|,|b_3|$这几个值都比较小。

## 代码

```C++
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N = 16;
const int O = 100;
int a1, a2, a3;
ll f[N+1][O+O];
ll g[N+1][O+O][O+O];
ll h[N+1][O+O][O+O][O+O];

ll f1(int n, int b) {
    ll &ans = f[n][b + O];
    if (ans != -1) return ans;
    if (n == N - 1) {
        if (b >= 0 && b <= 9) return ans = 1;
        else return ans = 0;
    }
    ans = 0;
    for (int m = (n == 0 ? 1 : 0); m < 10; m++) {
        if ((b - m) % a1 != 0) continue;
        ans += f1(n + 1, (b - m) / a1);
    }
    return ans;
}
ll f2(int n, int b1, int b2) {
    ll &ans = g[n][b1 + O][b2 + O];
    if (ans != -1) return ans;
    if (n == N - 1) {
        if (b1 >= 0 && b1 <= 9 && b1 == b2) return ans = 1;
        else return ans = 0;
    }
    ans = 0;
    for (int m = (n == 0 ? 1 : 0); m < 10; m++) {
        if ((b1 - m) % a1 != 0 || (b2 - m) % a2 != 0) continue;
        ans += f2(n + 1, (b1 - m) / a1, (b2 - m) / a2);
    }
    return ans;
}
ll f3(int n, int b1, int b2, int b3) {
    ll &ans = h[n][b1 + O][b2 + O][b3 + O];
    if (ans != -1) return ans;
    if (n == N - 1) {
        if (b1 >= 0 && b1 <= 9 && b1 == b2 && b2 == b3) return ans = 1;
        else return ans = 0;
    }
    ans = 0;
    for (int m = (n == 0 ? 1 : 0); m < 10; m++) {
        if ((b1 - m) % a1 != 0 || (b2 - m) % a2 != 0 || (b3 - m) % a3 != 0) continue;
        ans += f3(n + 1, (b1 - m) / a1, (b2 - m) / a2, (b3 - m) / a3);
    }
    return ans;
}
int main() {
    ll ans = 1;
    for (int i = 1; i < N; i++)
        ans *= 10;
    for (int i = 1; i < 10; i++) {
        a1 = -i;
        memset(f, -1, sizeof(f));
        ans += f1(0, 0);
    }
    for (int i = 1; i < 10; i++)
        for (int j = i + 1; i * j < 10; j++) {
            a1 = -i;
            a2 = -j;
            memset(g, -1, sizeof(g));
            ans -= f2(0, 0, 0);
        }
    for (int i = 1; i < 10; i++)
        for (int j = i + 1; i * j < 10; j++)
            for (int k = j + 1; i * j * k < 10; k++) {
                a1 = -i;
                a2 = -j;
                a3 = -k;
                memset(h, -1, sizeof(h));
                ans += f3(0, 0, 0, 0);
            }
    printf("%lld\n", ans);
}

```
