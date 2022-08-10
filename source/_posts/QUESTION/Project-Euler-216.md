---
title: Project Euler 216
category:
  - Project Euler
tags:
mathjax: true
date: 2022-06-02 21:04:10
---

<escape><!-- more --></escape>

# Project Euler 216

## 题目

### Investigating the primality of numbers of the form $2n^2-1$

Consider numbers $t(n)$ of the form $t(n) = 2n^2-1$ with $n > 1$.

The first such numbers are $7, 17, 31, 49, 71, 97, 127$ and $161$.

It turns out that only $49 = 7\times7$ and $161 = 7\times23$ are not prime.

For $n \le 10000$ there are $2202$ numbers $t(n)$ that are prime.

How many numbers $t(n)$ are prime for $n \le 50,000,000$ ?

## 解决方案

一个结论：如果$p\mid t(n)$，那么$p\mid t(kp\pm n)$，其中$k\ge0$。

原因：$t(kp\pm n)=2(kp^2\pm n)^2-1=2k^2p^4\pm4kp^2n+2n^2-1$。我们已经假定了$p\mid 2n^2-1$，因此$p\mid t(kp\pm n)$成立。

这说明只要发现$t(n)$有一个质因子$p$，就可以将它把$t(n+p),t(n+2p),\dots,t(p-n),t(2p-n),\dots$筛掉。

如果有一个数始终无法筛掉，说明它本身就是一个质数。

## 代码

```C++
#include <bits/stdc++.h>
typedef long long ll;
using namespace std;
const int N=50000000;
ll T[N+4];
int main(){
    int ans=0;
    for(int n=2;n<=N;n++)
        T[n]=2ll*n*n-1;
    for(int n=2;n<=N;n++){
        ll p=T[n];
        if(p==2ll*n*n-1) ++ans;
        if(p==1)
            continue;
        for(ll j=p+n;j<=N;j+=p)
            while(T[j]%p==0) T[j]/=p;
        for(ll j=p-n;j<=N;j+=p)
            while(T[j]%p==0) T[j]/=p;
    }
    printf("%d\n",ans);
}
```
