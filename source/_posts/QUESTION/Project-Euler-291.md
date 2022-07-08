---
title: Project Euler 291
tags:
  - Project Euler
mathjax: true
date: 2022-06-13 21:21:19
---

<escape><!-- more --></escape>

# Project Euler 291

## 题目

### Panaitopol Primes

A prime number $p$ is called a Panaitopol prime if $p = \dfrac{x^4 - y^4}{x^3 + y^3}$ for some positive integers $x$ and $y$.

Find how many Panaitopol primes are less than $5\times10^{15}$.

## 解决方案

令$g=\gcd(x,y)$，那么有$x=ga,y=gb$，其中$\gcd(a,b)=1$。

将上式写成$p(x^3+y^3)=x^4-y^4$，那么可以写成：

$$p(a^2-ab+b^2)=d(a^2+b^2)(a-b)$$

那么，$a^2-ab+b^2,(a^2+b^2)(a-b)$这两个数是互质的。

因此，$p=(a^2+b^2)(a-b),d=a^2-ab+b^2$。

但是，$p$是一个质数，但是有$a^2+b^2$和$a-b$两个质因式。因此$a-b=1$。

得到$p$是形如$p=a^2+(a+1)^2$的质数。

令$f(n)=2n^2+2n+1$

那么接下来使用和216题相似的筛法：如果$p|f(n)$，那么$p|f(kp+n),p|f(kp-n-1)$，其中$k>0$。

原因：$f(kp+n)=2(kp+n)^2+2(kp+n)+1 = 2k^2p^2+4knp+2kp+2n^2+2n+1$。我们已经假定了$p|2n^2+2n+1$，因此$p|f(kp+n)$成立。$p|f(kp-n-1)$的情况类似。

这说明只要发现$f(n)$有一个质因子$p$，就可以将它把$f(n+p),f(n+2p),\dots,f(p-n-1),t(2p-n-1),\dots$筛掉。

如果有一个数始终无法筛掉，说明它本身就是一个质数。

## 代码

```C++
#include <bits/stdc++.h>
typedef long long ll;
using namespace std;
const ll N=5e15;
const int M= sqrt(N/2)+10;
ll f[M+4];
int main(){
    int m;
    for(int i=1;i<=M;i++){
        f[i]=2ll*i*(i+1)+1;
        if(f[i]>=N){
            m=i-1;break;
        }
    }
    int ans=0;
    for(int i=1;i<=m;i++){
        ll p=f[i];
        if(p==2ll*i*(i+1)+1) ++ans;
        if(p==1) continue;
        for(ll j=p+i;j<=m;j+=p)
            while (f[j]%p==0) f[j]/=p;
        for(ll j=p-i-1;j<=m;j+=p)
            while (f[j]%p==0) f[j]/=p;
    }
    printf("%d\n",ans);
}
```
