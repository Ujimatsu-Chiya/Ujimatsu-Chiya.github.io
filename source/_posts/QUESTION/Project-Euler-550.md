---
title: Project Euler 550
category:
  - Project Euler
tags:
  - SG定理
  - 动态规划
  - 矩阵快速幂&#43;
mathjax: true
date: 2022-07-27 23:49:59
---

<escape><!-- more --></escape>

# Project Euler 550

## 题目

### Divisor game

Two players are playing a game. There are $k$ piles of stones. When it is his turn a player has to choose a pile and replace it by two piles of stones under the following two conditions:

- Both new piles must have a number of stones more than one and less than the number of stones of the original pile.
- The number of stones of each of the new piles must be a divisor of the number of stones of the original pile.

The first player unable to make a valid move loses.

Let $f(n,k)$ be the number of winning positions for the first player, assuming perfect play, when the game is played with k piles each having between $2$ and $n$ stones (inclusively).$f(10,5)=40085$.

Find $f(10^7,10^{12})$.Give your answer modulo $987654321$.

## 解决方案

令$N=10^7,Q=10^{12}$。

可以看出这是一个公平组合游戏，我们将每一堆石头视为独立的一个游戏局面，使用SG定理来解决本题。这里的石头一共有$k$堆，第$i$堆一共有$a_i$个，那么整个游戏的$sg$函数值为$sg(a_1)\oplus sg(a_2)\oplus\dots sg(a_k)$。

考虑目前的某一堆石头，一共有$n$个，每一次操作是用两堆石头$d_1,d_2$来代替它，这两堆石头是两个独立的新局面。因此，可以写出一堆石头的$sg$函数定义：

$$
sg(n)=
\left \{\begin{aligned}
  &0 & & \text{if\quad} n=1 \\
  &\text{mex}(\{sg(d_1)\oplus sg(d_2)|1<d_1\le d_2<n,d_1\mid n,d_2\mid n\}) & & \text{else}
\end{aligned}\right.
$$

其中运算$\text{mex}(s)$表示集合$s$中未出现的最小的非负整数。

可以发现，$1\sim N$中的$sg$函数值都很小（不超过$2^6$）。用一个数组$c[i]$表示$1\sim N$中有多少个数的$sg$函数值为$i$。

不过在实现的时候，直接枚举$1\sim N$中的所有因数再进行二重循环的效率是很低的。这里使用了一个优化方法：

对于$n$的分解$n=\prod_{i=1}^k p_i^{e_i}$而言，$sg(n)$只和**无序多重集**$\{e_i\}$有关，和$p_i$无关。因此，将$1\sim N$中的每个数分解质因数后对集合$\{e_i\}$进行哈希。只要哈希值相同，那么$sg$函数值一定相同。如果发现哈希值是第一次生成，那么才按照上面的二重循环计算$sg$函数值。经过实现，在这个数量级下，只有约$500$个不同的哈希值。

最终问题转化为有多少种方法可以将$sg$函数值填入一个长度为$Q$的序列，并且这$Q$个值的异或和不为$0$。

令状态$g(i,j)(0\le i\le Q,0\le j<2^6)$表示填入长度为$i$的序列，并且异或和为$j$的方案数有多少个。那么不难写出状态转移方程为：

$$
g(i,j)=
\left \{\begin{aligned}
  &1  & & \text{if\quad} i=0\land j=0 \\
  &0 & & \text{else if\quad} i=0 \\
  &\sum_{k=0}^{2^6-1} g(i-1,j\oplus k) \cdot c[k] & & \text{else}
\end{aligned}\right.
$$

但是，对于$Q$这种数据范围而言，直接进行转移效率非常低。

如果我们已经求出了长度为$a$的序列的各种填法$g(a,\cdot)$和长度为$b$的各种填法$g(b,\cdot)$，不难知道我们可以通过卷积组合出$g(a+b,\cdot)$。

枚举所有的$g(a,i)$和$g(b,j)$，将这两部分值直接合并起来：

$g(a,i)\cdot g(b,j)\rightarrow g(a+b,i\oplus j)$

因此，这给了我们一个方案：依次求出$g(2^0,\cdot),g(2^1,\cdot),g(2^2,\cdot),\dots$。然后针对$Q$，选择这些求出的$g(2^i,\cdot)$进行合并即可。

最终答案为$\sum_{i=1}^{2^6-1} g(Q,i)$。

## 代码

```C++
#include <bits/stdc++.h>
# include "tools.h"
using namespace std;
typedef long long ll;
const int N=10000000;
const ll Q=1e12;
ll mod=987654321;
int B=log2(N+1)+1;
const int M=1<<7;

int v[N+4],pr[N/10+100],m=0;
int sg[N+4];
bool mex[M];
int p[10],e[10],e2[10],o=0;
unordered_map<ll,int>sg_mem;
void fact(int n){
    o=0;
    for(;n!=1;){
        int x=v[n];
        p[++o]=x;
        e[o]=0;
        for(;n%x==0;n/=x,++e[o]);
    }
}
ll a[M],b[M];
void cal(ll a[M],ll b[M],ll ans[M]){
    ll c[M]={0};
    for(int i=0;i<M;i++)
        for(int j=0;j<M;j++)
            c[i^j]=(c[i^j]+a[i]*b[j])%mod;
    memcpy(ans,c,sizeof(c));
}
int main(){
    for(int i=2;i<=N;i++){
        if(v[i]==0){
            v[i]=i;pr[++m]=i;
        }
        for(int j=1;j<=m;j++){
            if(pr[j]>v[i]||pr[j]>N/i) break;
            v[i*pr[j]]=pr[j];
        }
    }
    for(int i=2;i<=N;i++){
        fact(i);
        memcpy(e2,e,sizeof(e));
        sort(e2+1,e2+o+1);
        ll hs=0;
        for(int j=1;j<=o;j++)
            hs=hs*B+e2[j];
        if(sg_mem.count(hs))
            sg[i]=sg_mem[hs];
        else{
            vector<pl>fact_v;
            for(int j=1;j<=o;j++)
                fact_v.push_back(pl(p[j],e[j]));
            vector<ll>d=divisors(fact_v);
            d.pop_back();
            d.erase(d.begin());
            memset(mex,0,sizeof(mex));
            for(int i=0;i<d.size();i++)
                for(int j=i;j<d.size();j++)
                    mex[sg[d[i]]^sg[d[j]]]=1;
            int j=0;
            for(;mex[j];++j);
            sg[i]=sg_mem[hs]=j;
        }
        ++b[sg[i]];

    }
    a[0]=1;
    for(ll n=Q;n;n>>=1){
        if(n&1) cal(a,b,a);
        cal(b,b,b);
    }
    ll ans=0;
    for(int j=1;j<M;j++)
        ans=(ans+a[j])%mod;
    printf("%lld\n",ans);
}

```
