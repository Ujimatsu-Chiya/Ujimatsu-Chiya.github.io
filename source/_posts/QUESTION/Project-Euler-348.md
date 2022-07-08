---
title: Project Euler 348
tags:
  - Project Euler
mathjax: true
date: 2022-07-08 17:06:29
---

<escape><!-- more --></escape>

# Project Euler 348

## 题目

### Sum of a square and a cube

Many numbers can be expressed as the sum of a square and a cube. Some of them in more than one way.

Consider the palindromic numbers that can be expressed as the sum of a square and a cube, both greater than $1$, in **exactly** $4$ different ways.

For example, $5229225$ is a palindromic number and it can be expressed in exactly $4$ different ways:

$\begin{aligned}
& 2285^2 + 20^3\\
& 2223^2 + 66^3\\
& 1810^2 + 125^3\\
& 1197^2 + 156^3\\
\end{aligned}$

Find the sum of the five smallest such palindromic numbers.

## 解决方案

本题的解决方式比直接。先从小到大生成$2$位以上的回文数，然后再通过枚举立方数，判断减去后的数是否为平方数即可。

## 代码

```C++
# include <bits/stdc++.h>
# include "tools.h"
using namespace std;
typedef long long ll;
const int M=4,Q=5;
ll rev(ll n){
    ll s=0;
    for(;n;n/=10) s=s*10+n%10;
    return s;
}
bool ok(ll n){
    int cnt=0;
    for(ll i=1;i*i*i<=n;i++)
        if(is_square(n-i*i*i)) ++cnt;
    return cnt==M;
}
ll ans=0;
void solve(){
    int cnt=0;
    for(ll l=1;;l*=10){
        ll r=l*10;
        for(ll i=l;i<r;i++){
            ll w=i*r+rev(i);
            if(ok(w)){
                ans+=w;
                ++cnt;if(cnt==Q) return;
            }
        }
        for(ll i=l;i<r;i++){
            for(int j=0;j<10;j++){
                ll w=(i*10+j)*r+rev(i);
                if(ok(w)){
                    ans+=w;
                    ++cnt;if(cnt==Q) return;
                }
            }
        }
    }
}
int main(){
    solve();
    printf("%lld\n",ans);
}

```
