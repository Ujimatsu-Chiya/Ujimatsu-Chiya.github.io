---
title: Project Euler 333
tags:
  - Project Euler
mathjax: true
date: 2022-07-27 23:50:26
---

<escape><!-- more --></escape>

# Project Euler 333

## 题目

### Special partitions

All positive integers can be partitioned in such a way that each and every term of the partition can be expressed as $2^i\times3^j$, where $i,j \ge 0$.

Let’s consider only those such partitions where none of the terms can divide any of the other terms.

For example, the partition of $17 = 2 + 6 + 9 = (2^1\times3^0 + 2^1\times3^1 + 2^0\times3^2)$ would not be valid since $2$ can divide $6$. Neither would the partition $17 = 16 + 1 = (2^4\times3^0 + 2^0\times3^0)$ since $1$ can divide $16$. The only valid partition of $17$ would be $8 + 9 = (2^3\times3^0 + 2^0\times3^2)$.

Many integers have more than one valid partition, the first being 11 having the following two partitions.

$11 = 2 + 9 = (2^1\times3^0 + 2^0\times3^2)$
$11 = 8 + 3 = (2^3\times3^0 + 2^0\times3^1)$

Let’s define $P(n)$ as the number of valid partitions of $n$. For example, $P(11) = 2$.

Let’s consider only the prime integers $q$ which would have a single valid partition such as $P(17)$.

The sum of the primes $q <100$ such that $P(q)=1$ equals $233$.

Find the sum of the primes $q <1000000$ such that $P(q)=1$.

## 解决方案

如果$n$的一个划分为$2^{e_1}3^{f_1}+2^{e_2}3^{f_2}+\dots$是有效的，那么不能存在一对$e_i,e_j$或$f_i,f_j$满足$e_i=e_j$或$f_i=f_j$，并且不能够同时满足$e_i<e_j,f_i,f_j$。因此假设$e_1< e_2< e_3< \dots$，那么必须有$f_1>f_2>f_3>\dots$

令$N=10^6,M=\lceil\log_3 N\rceil+1,O=\lfloor\log _2N\rfloor$。考虑用动态规划解决本问题。令状态$f(i,j,k)(-1\le i\le O,0\le j< N,0\le k\le M)$表示当前对数$j$的有效划分方法中，满足$e_1<e_2<\dots\le i,f_1>f_2>\dots \ge k$的方法数。需要注意的是，这里的$i=-1$这个状态并非真正存在，仅仅是为了定初值，然后进行转移。

那么对于$i=-1,f(i,0,M)=1$。对于$i=-1$的其它情况，则为$0$。

这里的动态规划使用我为人人的形式。对于任意一个状态$f(i,j,k)$，有以下转移：

- $f(i,j,k)\rightarrow f(i+1,j,k)$，这个转移方式说明序列$e$不会存在$x$使得$e_x=i+1$。
- 对于所有$l< k,j+2^{i+1}3^l< N$，都有$f(i,j,k)\rightarrow f(i+1,j+2^{i+1}3^l,l)$，这说明$j$再加上一个数$2^{i+1}3^l$就变成了$j+2^{i+1}3^l$的一个划分方案，并且还是**保持有效**的。

那么，最终答案为

$$P(n)=\sum_{k=0}^M f(O,n,k)$$

## 代码

```C++
#include <bits/stdc++.h>
typedef long long ll;
using namespace std;
const int N=1000000;
const int M=log(N+1)/log(3)+2;
vector<int>pw23[36];
int f[N+4][M];
bool vis[N+4];
int pr[N/10+100],m=0;
int main(){
    for(int i=2;i<N;i++){
        if(vis[i]) continue;
        pr[++m]=i;
        for(ll j=1ll*i*i;j<N;j+=i)
            vis[j]=1;
    }
    for(int i=0;(1<<i)<N;i++){
        int x=(1<<i);
        for(int j=0;;j++){
            pw23[i].push_back(x);
            x*=3;
            if(x>=N) break;
        }
    }
    f[0][M-1]=1;
    for(int i=0;(1<<i)<N;i++){
        for(int j=N;j>=0;j--){
            for(int k=0;k<M;k++){
                if(f[j][k]==0) continue;
                for(int l=0;l<pw23[i].size()&&l<k&&j+pw23[i][l]<=N;l++){
                    f[j+pw23[i][l]][l]+=f[j][k];
                }
            }
        }
    }
    ll ans=0;
    for(int i=1;i<=m;i++){
        int p=pr[i],c=0;
        for(int j=0;j<M;j++)
            c+=f[p][j];
        if(c==1) ans+=p;
    }
    printf("%lld\n",ans);
}

```
