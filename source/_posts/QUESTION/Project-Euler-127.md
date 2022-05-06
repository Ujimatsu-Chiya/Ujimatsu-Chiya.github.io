---
title: Project Euler 127
tags:
  - Project Euler
mathjax: true
date: 2022-05-06 22:25:02
---

<escape><!-- more --></escape>

# Project Euler 127

## 题目

### abc-hits

The radical of $n$, $\mathrm{rad}(n)$, is the product of the distinct prime factors of $n$. For example, $504 = 2^3 × 3^2 × 7$, so $\mathrm{rad}(504) = 2 × 3 × 7 = 42$.

We shall define the triplet of positive integers $(a, b, c)$ to be an $abc$-hit if:

1. $\gcd(a, b) = \gcd(a, c) = \gcd(b, c) = 1$
2. $a < b$
3. $a + b = c$
4. $\mathrm{rad}(abc) < c $;

For example, $(5, 27, 32)$ is an abc-hit, because:

1. $\gcd(5, 27) = \gcd(5, 32) = \gcd(27, 32) = 1$
2. $5 < 27$
3. $5 + 27 = 32$
4. $\mathrm{rad}(4320) = 30 < 32$

It turns out that abc-hits are quite rare and there are only thirty-one abc-hits for $c < 1000$, with $\sum c = 12523$.

Find $\sum c$ for $c < 120000$.

## 解决方案

按照第124题的方式计算出所有$\mathrm{rad}$的值。

如果第三条成立，那么就有：$a,b,c$三个值，任意一个可以由另外两个**线性表出**。因为这个特性，如果$a,b,c$三个值两两互质，只需要判断其中一对值是否互质即可。

根据$\mathrm{rad}(n)$的定义，是由$n$的不同的质因数相乘得出的值。那么由于$a,b,c$两两互质，它们之间没有相同的质因数，因此$\mathrm{rad}(abc)=\mathrm{rad}(a)\cdot \mathrm{rad}(b)\cdot \mathrm{rad}(c)$。

这给我们提供了一个思路，首先将$1\sim N$中的所有值按照函数值$\mathrm{rad}$从小到大排序。先从小到大枚举$c$的值，然后再按照$\mathrm{rad}$的大小从小到大枚举$a$的值。当$\mathrm{rad}(a)\cdot \mathrm{rad}(c)\ge c$时，就可以停止枚举$a$了。剩下的就是判断其它答案是否符合条件。

## 代码

```C++
# include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N=120000-1;
int rad[N+4],rk[N+4];
int main(){
    for(int i=1;i<=N;i++)
        rk[i]=i,rad[i]=1;
    for(int i=2;i<=N;i++){
        if(rad[i]==1){
            for(int j=i;j<=N;j+=i)
                rad[j]*=i;
        }
    }
    sort(rk+1,rk+N+1,[&](int &x,int &y){
         return rad[x]<rad[y]||rad[x]==rad[y]&&x<y;
         });
    ll ans=0;
    for(int c=1;c<=N;c++){
        for(int i=1;i<=N;i++){
            int a=rk[i];
            if(rad[a]*rad[c]>=c)
                break;
            if(__gcd(a,c)!=1) continue;
            int b=c-a;
            if(a<b && 1ll*rad[a]*rad[b]*rad[c]<c)
                ans+=c;
        }
    }
    printf("%lld\n",ans);
}

```
