---
title: Project Euler 531
category:
  - Project Euler
tags:
  - 中国剩余定理
mathjax: true
date: 2022-07-13 22:57:33
---

<escape><!-- more --></escape>

# Project Euler 531

## 题目

### Chinese leftovers

Let $g(a,n,b,m)$ be the smallest non-negative solution $x$ to the system:

$\begin{aligned}
& x = a \bmod n\\
& x = b \bmod m
\end{aligned}$

if such a solution exists, otherwise $0$.

E.g. $g(2,4,4,6)=10$, but $g(3,4,4,6)=0$.

Let $\varphi(n)$ be Euler’s totient function.

Let $f(n,m)=g(\varphi(n),n,\varphi(m),m)$.

Find $\sum f(n,m)$ for $1000000 \le n < m < 1005000$.

## 解决方案

题意比较裸，直接求出欧拉函数值然后通过中国剩余定理求方程的解即可。

当然也可以令$x=t_an+a=t_bm+b$，那么可以写出方程$t_an-t_bm=b-a$，只需要用一次扩展欧几里得算法就可以求出$t_a,t_b$，从而重新计算出$x$。这种做法比起使用中国剩余定理，少使用了一次扩展欧几里得算法，故也可以考虑。

## 代码

```C++
# include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const int L=1000000,R=1005000;
int phi[R+4];
ll ex_gcd(ll a,ll b,ll &x,ll &y){
    if(b==0){
        x=1;y=0;return a;
    }
    ll g=ex_gcd(b,a%b,x,y);
    ll z=x-(a/b)*y;
    x=y;y=z;return g;
}
//解不定方程ax+my=c。
ll congruence(ll a,ll c,ll m){
    ll x,y,g;
    g=ex_gcd(a,m,x,y);
    if(c%g!=0) return -1;
    x*=c/g;
    ll t=m/g;
    return (x%t+t)%t;
}
ll CRT(ll b,ll m,ll c,ll n){
    ll y=congruence(m,c-b,n);
    if(y==-1) return -1;
    ll x=m*y+b;
    ll t=m*n;
    return (x%t+t)%t;
}
int main(){
    for(int i=1;i<R;i++)
        phi[i]=i;
    for(int i=2;i<R;i++){
        if(phi[i]!=i) continue;
        phi[i]=i-1;
        for(int j=i+i;j<R;j+=i)
            phi[j]=phi[j]/i*(i-1);
    }
    ll ans=0;
    for(int i=L;i<R;i++){
        for(int j=i+1;j<R;j++){
            ll x=CRT(phi[i],i,phi[j],j);
            if(x!=-1) ans+=x;
        }
    }
    printf("%lld\n",ans);
}

```
