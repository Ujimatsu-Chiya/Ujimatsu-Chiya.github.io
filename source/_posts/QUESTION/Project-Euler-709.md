---
title: Project Euler 709
category:
  - Project Euler
tags:
mathjax: true
date: 2022-06-22 23:27:13
---

<escape><!-- more --></escape>

# Project Euler 709

## 题目

### Even Stevens

Every day for the past $n$ days Even Stevens brings home his groceries in a plastic bag. He stores these plastic bags in a cupboard. He either puts the plastic bag into the cupboard with the rest, or else he takes an **even** number of the existing bags (which may either be empty or previously filled with other bags themselves) and places these into the current bag.

After $4$ days there are $5$ possible packings and if the bags are numbered $1$ (oldest), $2, 3, 4$, they are:

- Four empty bags,
- $1$ and $2$ inside $3, 4$ empty,
- $1$ and $3$ inside $4, 2$ empty,
- $1$ and $2$ inside $4, 3$ empty,
- $2$ and $3$ inside $4, 1$ empty.

Note that $1, 2, 3$ inside $4$ is invalid because every bag must contain an even number of bags.

Define $f(n)$ to be the number of possible packings of $n$ bags. Hence $f(4)=5$. You are also given $f(8)=1\,385$.

Find $f(24\,680)$ giving your answer modulo $1\,020\,202\,009$.

## 解决方案

考虑以动态规划的思想计算$f(n)$，那么可以列出如下状态转移方程：

$$
f(n)=
\left \{\begin{aligned}
  &1  & & \mathrm{if\quad} n=0|n=1 \\
  &f(n)=\sum_{k=0}^{\lfloor\frac{n-1}{2}\rfloor}C_{n-1}^{2k}\cdot f(2k)\cdot f(n-1-2k) & & \mathrm{else}
\end{aligned}\right.
$$

解释：可以发现，这些塑料袋的嵌套关系可以用一棵树来描述：

- 如果$A$装了$B,C$，那么$B,C$就是$A$的子节点。
- 如果$B$又装了其它$D,E$，那么$A$也是$D,E$的祖先节点。
- $A$的**子树**就包括其所有的后代节点（不包括自身）。

由于题目要求每一个节点都必须有偶数个子节点，因此任何一棵子树都有偶数个子节点。那么，$f(n)$的含义就变成：$n$个节点可以构成多少种满足以上要求的树的集合（森林）？

当第$n$个节点到来时，考虑任意选择将$2k$“包裹”在第$n$个节点下，而这$2k$个节点任意组成的森林种类为$f(2k)$种，节点$n$最终将这$2k$个节点形成的森林练成一棵树；剩下的$n-1-2k$个节点中，它们也可以任意组成森林，有$f(n-1-2k)$种。这三个步骤是独立的，故得到以上状态转移方程。

顺带一提，暴力枚举出前几项后，查询OEIS，发现结果为[A000111](https://oeis.org/A000111)。在FORMULA一栏中找到了如下信息：

```
2*a(n+1) = Sum_{k=0..n} binomial(n, k)*a(k)*a(n-k).
```

这给出了$f(n)$的另一条递推公式：

$$f(n+1)=\dfrac{\sum_{k=0}^nC_n^k\cdot f(k)\cdot f(n-k)}{2}$$

## 代码

```C++
# include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N=24680;
int mod=1020202009;
ll fac[N+4],finv[N+4],inv[N+4];
ll C(int n,int m){
    return 1ll*fac[n]*finv[m]%mod*finv[n-m]%mod;
}
ll f[N+4];
int main(){
    fac[0]=fac[1]=inv[1]=finv[0]=finv[1]=1;
    for(int i=2;i<=N;i++){
        fac[i]=fac[i-1]*i%mod;
        inv[i]=(mod-mod/i)*inv[mod%i]%mod;
        finv[i]=finv[i-1]*inv[i]%mod;
    }
    f[0]=f[1]=1;
    for(int n=1;n<N;n++){
        for(int k=0;k<=n;k+=2)
            f[n+1]=(f[n+1]+1ll*C(n,k)*f[k]%mod*f[n-k])%mod;
    }
    printf("%lld\n",f[N]);
}
```
