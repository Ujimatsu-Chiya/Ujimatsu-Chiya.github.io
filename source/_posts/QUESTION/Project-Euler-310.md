---
title: Project Euler 310
category:
  - Project Euler
tags:
  - 博弈论
  - SG定理
mathjax: true
date: 2022-07-06 13:08:59
---

<escape><!-- more --></escape>

# Project Euler 310

## 题目

### Nim Square

Alice and Bob play the game Nim Square.

Nim Square is just like ordinary three-heap normal play Nim, but the players may only remove a square number of stones from a heap.

The number of stones in the three heaps is represented by the ordered triple $(a,b,c)$.

If $0\le a\le b\le c\le29$ then the number of losing positions for the next player is $1160$.

Find the number of losing positions for the next player if $0\le a\le b\le c\le100 000$.

## Sprague–Grundy定理

$sg$函数是一个用来解决公平组合游戏(ICG)问题的一种工具。

定义一个非负整数集合上的运算$\text{mex}(s)$：表示集合$s$中未出现的最小的非负整数。

我们定义一个游戏状态$n$，令$sg(n)=\text{mex}(\{sg(m)|n\rightarrow m\})$.$m$是从$n$能够抵达的所有游戏状态。如果$sg(n)>0$，那么状态$n$为必胜态；如果$sg(n)=0$，那么为必败态。

[Sprague–Grundy，SG定理](https://en.wikipedia.org/wiki/Sprague%E2%80%93Grundy_theorem)说明了，如果这个游戏当前的状态$n$，它可以看做是多个状态$(n_1,n_2,\dots,n_k)$的组合，那么就可以写成：

$$sg(n)=sg(n_1)\oplus sg(n_2)\oplus \dots \oplus sg(n_k)$$

以NIM游戏为例，如果当前有$n$堆石头，其中第$i$堆为$a_i$。那么状态$sg(a_1,a_2,\dots,a_n)$可以看成是$sg(a_1),sg(a_2),\dots,sg(a_n)$的组合，当前的状态是必胜态还是必败态由$sg(a_1)\oplus sg(a_2)\oplus\dots\oplus sg(a_n)$决定。

因此一般使用SG定理解决问题，主要依靠的是分治的思想。

## 解决方案

在每一次操作中，一方可以拿起三堆石头$(a,b,c)$的其中一堆的石头的平方数个。并且这$3$堆石头是相互独立的。因此，三堆石头的$sg$函数$sg(a,b,c)=sg(a)\oplus sg(b)\oplus sg(c)$.那么此时只需要单独考虑一堆石头的情况$sg(n)$。

只拿一堆石头时，那么剩下的石头只可能为$n-1^2,n-2^2,n-3^2,\dots$。那么不难写出$sg(n)$为：

$$
sg(n)=
\left \{\begin{aligned}
  &0 & & \mathrm{if\quad} n=0 \\
  &\text{mex}(\{sg(n-i^2)|1\le i^2\le n\}) & & \mathrm{else}
\end{aligned}\right.
$$

由此可以快速地求出每个独立状态的$sg$值。

令$N=10^5$，那么问题就转化成有多少个三元组$(a,b,c),0\le a\le b\le c\le N$，满足$sg(a)\oplus sg(b)\oplus sg(c)=0$。

可以想到先统计在$0\sim N$中有多少个值$n$，其中有$c(i)$个$n$满足$sg(n)=i$。令$O=\max_{i=0}^N sg(i)$。并且其实$O$值很小。那么可以考虑通过枚举$i,j$使得$0\le i\le j\le i\oplus j \le O$，进行组合计数即可。计数的过程中要注意当$i=j$时，$c[i]$和$c[j]$使用的是同一个部分下的所有数。

## 代码

```C++
# include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N=100000;
const int M=log(N+10)*10+10;
int sg[N+4];
bool mex[M+4];
int cnt[M+4];
int main(){
    for(int i=1;i<=N;i++){
        memset(mex,0,sizeof(mex));
        for(int j=1;j*j<=i;j++)
            mex[sg[i-j*j]]=1;
        int j=0;
        for(;mex[j];++j);
        sg[i]=j;
        ++cnt[sg[i]];
    }
    ++cnt[0];
    int mx=*max_element(sg+1,sg+N+1);
    ll ans=0;
    for(int i=0;i<=mx;i++)
        for(int j=i+1;j<=mx;j++){
            int k=i^j;
            if(mx>=k&&k>j)
                ans+=1ll*cnt[i]*cnt[j]*cnt[k];
        }
    for(int i=1;i<=mx;i++)
        ans+=1ll*cnt[i]*(cnt[i]+1)/2*cnt[0];
    ans+=1ll*cnt[0]*(cnt[0]+1)*(cnt[0]+2)/6;
    printf("%lld\n",ans);
}

```
