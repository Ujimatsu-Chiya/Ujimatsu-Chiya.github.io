---
title: Project Euler 378
category:
  - Project Euler
tags:
  - 动态规划
  - 树状数组
mathjax: true
date: 2022-07-27 23:50:51
---

<escape><!-- more --></escape>

# Project Euler 378

## 题目

### Triangle Triples

Let $T(n)$ be the $n^\text{th}$ triangle number, so $T(n) = \dfrac{n(n + 1)}{2}$.

Let $dT(n)$ be the number of divisors of $T(n)$.

E.g.: $T(7) = 28$ and $dT(7) = 6$.

Let $Tr(n)$ be the number of triples $(i, j, k)$ such that $1 \le i \lt j \lt k \le n$ and $dT(i) \gt dT(j) \gt dT(k)$

$Tr(20) = 14$, $Tr(100) = 5772$, and $Tr(1000) = 11174776$.

Find $Tr(60 000 000)$.

Give the last $18$ digits of your answer.

## 解决方案

令$N=600000000$，通过线性筛预处理处理出$1\sim N+1$的因数个数，可以以$O(N)$的时间复杂度计算出所有$dT$值，令$M$是$1\sim N$中$dT$值最大的一个。

考虑使用动态规划的思想解决本题。令状态$(i,j)(1\le i\le 3,1\le j\le N)$表示长度为$i$并且以$j$为结尾的序列有多少个（即$p_1<p_2<\dots<p_{i-1}<j$ 并且$dT(p_1)>dT(p_2)>\dots>dT(p_{i-1})>j$）

那么不难写出关于$f(i,j)$的状态转移方程：

$$
f(i,j)=
\left \{\begin{aligned}
  &1  & & \text{if}\quad i=1 \\
  &\sum_{k<j,dT(k)>j} f(i-1,k) & & \text{else}
\end{aligned}\right.
$$

直接进行转移的效率非常低，因此考虑使用树状数组维护状态：将当前所有$f(i-1,k),k\le j$的状态都按照值$dT(k)$存到树状数组中，那么询问时只需要以$O(\log M)$的时间复杂度求得大于$dT(j)$的所有状态之和。

最终答案为$\sum_{j=1}^Nf(3,j)$，时间复杂度为$O(N\log M)$。

## 代码

```C++
#include <bits/stdc++.h>
# define lb(i) ((i)&(-i))
typedef long long ll;
using namespace std;
const int N=60000000;
ll mod=1e18;
int M=0;
int v[N+4],pr[N/10+100],m=0;
int d[N+4];
ll s[N+4],f[N+4];
void pl(ll &x,ll y){
    x+=y;
    if(x>=mod) x-=mod;
}
void add(int p,ll x){
    for(int i=p;i<=M;i+=lb(i)){
        pl(s[i],x);
    }
}
ll que(int p){
    ll a=0;
    for(int i=p;i;i-=lb(i))
        pl(a,s[i]);
    return a;
}
int main(){
    f[1]=1;
    for(int i=2;i<=N+1;i++){
        if(v[i]==0){
            v[i]=i;pr[++m]=i;f[i]=2;
        }
        for(int j=1;j<=m;j++){
            if(pr[j]>v[i]||pr[j]>(N+1)/i) break;
            v[i*pr[j]]=pr[j];
            f[i*pr[j]]=f[i]*2-(pr[j]==v[i]?f[i/pr[j]]:0);
        }
    }
    for(int n=1;n<=N;n++)
        d[n]=n&1?f[n]*f[(n+1)>>1]:f[n>>1]*f[n+1];
    M=*max_element(d+1,d+N+1);
    for(int i=1;i<=N;i++)
        f[i]=1;
    for(int k=1;k<=2;k++){
        memset(s,0,sizeof(s));
        ll sum=0;
        for(int i=1;i<=N;i++){
            ll x=f[i];
            f[i]=sum-que(d[i]);
            add(d[i],x);
            pl(sum,x);
        }
    }
    ll ans=0;
    for(int i=1;i<=N;i++)
        pl(ans,f[i]);
    printf("%lld\n",ans);
}

```
