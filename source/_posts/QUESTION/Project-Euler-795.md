---
title: Project Euler 795
category:
  - Project Euler
tags:
mathjax: true
date: 2022-07-19 00:28:53
---

<escape><!-- more --></escape>

# Project Euler 795

## 题目

### Alternating GCD Sum

For a positive integer $n$, the function $g(n)$ is defined as

$$\displaystyle g(n)=\sum_{i=1}^{n} (-1)^i \gcd \left(n,i^2\right)$$

For example, $g(4) = -\gcd \left(4,1^2\right) + \gcd \left(4,2^2\right) - \gcd \left(4,3^2\right) + \gcd \left(4,4^2\right) = -1+4-1+4=6$.<br />
You are also given $g(1234)=1233$.

Let $\displaystyle G(N) = \sum_{n=1}^N g(n)$. You are given $G(1234) = 2194708$.

Find $G(12345678)$.

## 解决方案

$$\begin{aligned}
G(N)&=\sum_{n=1}^N\sum_{i=1}^n(-1)^i\gcd(n,i^2)=\sum_{i=1}^N(-1)^i(\sum_{n=i}^N\gcd(n,i^2))
\end{aligned}$$

其中对于右边那一块，有：

$$\sum_{n=1}^N\gcd(n,i^2)=\sum_{d|i^2}\lfloor\dfrac{N}{d}\rfloor\cdot (\sum_{e|d}\mu(\dfrac{d}{e})\cdot e)=\sum_{d|i^2}\lfloor\dfrac{N}{d}\rfloor\cdot\varphi(d) $$

那么将$G(n)$可以继续重新改写，有：

$$\begin{aligned}
G(N)&=\sum_{i=1}^N(-1)^i(\sum_{d|i^2}\varphi(d)\cdot (\lfloor\dfrac{N}{d}\rfloor-\lfloor\dfrac{i-1}{d}\rfloor)\\
&=\sum_{d=1}^N\varphi(d)(\sum_{d|i^2}(-1)^i\cdot (\lfloor\dfrac{N}{d}\rfloor-\lfloor\dfrac{i-1}{d}\rfloor))
\end{aligned}$$

那么通过筛法实现计算$G$即可。令$n$的分解为$n=\prod_{k=1}^mp_i^{e_i}$，那么如果一个数$m$满足$n|m^2$，那么就满足$n'|m$，其中$n'=\prod_{k=1}^mp_i^{\lceil\frac{e_i}{2}\rceil}$。

最终时间复杂度为$O(N\log N)$，略慢。

以后再思考如何使用亚线性算法进行优化。

## 代码

```C++
#include <bits/stdc++.h>
typedef long long ll;
using namespace std;
const int N=12345678;
int v[N+4],phi[N+4];
int pr[N/10+100],m=0;
int cal(int n){
    int m=1;
    for(;n!=1;){
        for(int c=0,p=v[n];n%p==0;n/=p,c^=1)
            if(!c) m*=p;
    }
    return m;
}
int main(){
    phi[1]=1;
    for(int i=2;i<=N;i++){
        if(v[i]==0){
            pr[++m]=i;phi[i]=i-1;v[i]=i;
        }
        for(int j=1;j<=m;j++){
            if(pr[j]>v[i]||pr[j]>N/i) break;
            v[i*pr[j]]=pr[j];
            phi[i*pr[j]]=phi[i]*(pr[j]==v[i]?pr[j]:pr[j]-1);
        }
    }
    ll ans=0;
    for(int d=1;d<=N;d++){
        int k=cal(d);
        for(int i=k;i<=N;i+=k){
            if(i&1) ans-=phi[d]*(N/d-(i-1)/d);
            else ans+=phi[d]*(N/d-(i-1)/d);
        }
    }
    printf("%lld\n",ans);
}


```
