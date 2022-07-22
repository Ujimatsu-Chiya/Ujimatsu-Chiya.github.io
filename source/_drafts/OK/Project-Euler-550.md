---
title: Project Euler 550
tags:
  - Project Euler
  - SG定理
  - 矩阵快速幂&#43;
mathjax: true
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