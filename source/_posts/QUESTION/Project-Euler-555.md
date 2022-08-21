---
title: Project Euler 555
category:
  - Project Euler
mathjax: true
date: 2022-08-21 23:50:49
tags:
---

<escape><!-- more --></escape>

# Project Euler 555

## 题目

### McCarthy $91$ function

The McCarthy 91 function is defined as follows:
$$
M_{91}(n) =
    \begin{cases}
        n - 10 & \text{if } n > 100 \\
        M_{91}(M_{91}(n+11)) & \text{if } 0 \leq n \leq 100
    \end{cases}
$$

We can generalize this definition by abstracting away the constants into new variables:

$$
M_{m,k,s}(n) =
    \begin{cases}
        n - s & \text{if } n > m \\
        M_{m,k,s}(M_{m,k,s}(n+k)) & \text{if } 0 \leq n \leq m
    \end{cases}
$$

This way, we have $M_{91} = M_{100,11,10}$.

Let $F_{m,k,s}$ be the set of fixed points of $M_{m,k,s}$. That is,

$$F_{m,k,s}= \left\{ n \in \mathbb{N} \, | \, M_{m,k,s}(n) = n \right\}$$

For example, the only fixed point of $M_{91}$ is $n = 91$. In other words, $F_{100,11,10}= \{91\}$.

Now, define $SF(m,k,s)$ as the sum of the elements in $F_{m,k,s}$ and let $S(p,m) = \displaystyle \sum_{1 \leq s < k \leq p}{SF(m,k,s)}$.

For example, $S(10, 10) = 225$ and $S(1000, 1000)=208724467$.

Find $S(10^6, 10^6)$.

## 解决方案

使用以下程序，调整参数$m,k,s$进行打表：

```py
m = 203
k = 12
s = 8


def f(n):
    if n > m:
        return n - s
    else:
        return f(f(n + k))


for n in range(m + 4):
    print(n, f(n))

```

发现如下信息：

- 当$n\le m$时，$M_{m,k,s}(n)$是周期性的，其周期为$k-s$。
- $M_{m,k,s}(m)=m-2s+k$。

如果存在$n$，使得$M_{m,k,s}(n)=n$，那么就意味着$m-2s+k\equiv m \pmod{k-s}$。化简后，得到

$$k\equiv 0 \pmod {k-s}$$

也就是说，只有满足$k-s\mid k$时，$M_{m,k,s}(n)$中一整个周期都是方程$M_{m,k,s}(n)=n$的解。这些解的范围是以下区间中的整数：

$$(m-(2s-k)-(k-s),m-(2s-k)]$$

因此先枚举$d$值，再枚举$d$的倍数$k$，那么取$s=k-d$，回代到区间的式子中，计算这个区间中**非负整数**之和即可。

## 代码

```C++
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N=1000000,M=1000000;
int main(){
    ll ans=0;
    for(int d=1;d<=N;d++){
        for(int k=d+d;k<=N;k+=d){
            int s=k-d;
            int st=M-s-s+k;
            int cnt=max(0,min(k-s,M-s-s+k+1));
            ans+=1ll*(st+st-cnt+1)*cnt/2;
        }
    }
    printf("%lld\n",ans);
}

```
