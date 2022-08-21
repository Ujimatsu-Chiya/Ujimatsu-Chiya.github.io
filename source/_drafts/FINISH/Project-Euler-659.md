---
title: Project Euler 659
category:
  - Project Euler
tags:
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 659
## 题目
### Largest prime



Consider the sequence  $n^2+3$ with $n \ge 1$. 
If we write down the first terms of this sequence we get:

$4, 7, 12, 19, 28, 39, 52, 67, 84, 103, 124, 147, 172, 199, 228, 259, 292, 327, 364,\dots.$

We see that the terms for $n=6$ and $n=7$ ($39$ and $52$) are both divisible by $13$.

In fact $13$ is the largest prime dividing any two successive terms of this sequence.


Let $P(k)$ be the largest prime  that divides any two successive terms of the sequence $n^2+k^2$.

Find the last $18$ digits of $\displaystyle \sum_{k=1}^{10\,000\,000} P(k)$.



## 解决方案

根据题意，所求质数$p$必须保证存在$n$，使得下式成立：

$$
\left \{\begin{aligned}
& n^2+k^2\equiv 0 &\pmod p \qquad(1)\\
& (n+1)^2+k^2\equiv 0 &\pmod p \qquad(2)
\end{aligned}\right.
$$

对$(2)$减去$(1)$，得到$2n\equiv -1\pmod p$。

对式子两边进行平方，得到$4n^2\equiv 1\pmod p$。

将式子和$(1)$重新联立，消去$n$，得到$4k^2+1\equiv 0 \pmod p$。

也就是说，$P(k)$为$4k^2+1$的最大质因数。

最终采用和216题类似的筛法计算$P(k)$：如果$p\mid P(k)$，那么$p\mid P(tp\pm k)$。

## 代码


```C++
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N=10000000;
ll mod=1000000000000000000;
ll f[N+4],a[N+4];
int main(){
    for(int n=1;n<=N;n++)
        f[n]=4ll*n*n+1;
    for(int n=1;n<=N;n++){
        ll p=f[n];
        if(p==1) continue;
        a[n]=max(a[n],p);
        for(ll j=p+n;j<=N;j+=p){
            a[j]=max(a[j],p);
            while(f[j]%p==0) f[j]/=p;
        }
        for(ll j=p-n;j<=N;j+=p){
            a[j]=max(a[j],p);
            while(f[j]%p==0) f[j]/=p;
        }
    }
    ll ans=0;
    for(int i=1;i<=N;i++)
        ans=(ans+a[i])%mod;
    printf("%lld\n",ans);
}

```