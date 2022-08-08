---
title: Project Euler 425
category:
  - Project Euler
tags:
  - 并查集
mathjax: true
date: 2022-07-12 00:16:59
---

<escape><!-- more --></escape>

# Project Euler 425

## 题目

### Prime connection

Two positive numbers $A$ and $B$ are said to be *connected* (denoted by "$A \leftrightarrow B$") if one of these conditions holds:

(1) $A$ and $B$ have the same length and differ in exactly one digit; for example, $123 \leftrightarrow 173$.

(2) Adding one digit to the left of $A$ (or $B$) makes $B$ (or $A$); for example, $23 \leftrightarrow 223$ and $123 \leftrightarrow 23$.

We call a prime $P$ a *$2$'s relative* if there exists a chain of connected primes between $2$ and $P$ and no prime in the chain exceeds $P$.

For example, $127$ is a $2$'s relative. One of the possible chains is shown below:

$2 \leftrightarrow 3 \leftrightarrow 13 \leftrightarrow 113 \leftrightarrow 103 \leftrightarrow 107 \leftrightarrow 127$

However, $11$ and $103$ are not $2$'s relatives.

Let $F(N)$ be the sum of the primes $\le N$ which are not $2$'s relatives.

We can verify that $F(10^3) = 431$ and $F(10^4) = 78728$.

Find $F(10^7)$.

## 并查集

[并查集](https://en.wikipedia.org/wiki/Disjoint-set_data_structure)：用于高效处理一些不相交集合的数据结构。一般有两个操作：合并两个集合；查询两个元素是否在同一个集合中。

可以通过优化将并查集这两种单次操作优化到$O(\alpha(n))$级别，其中$\alpha(n)$是[反阿克曼函数](https://en.wikipedia.org/wiki/Ackermann_function#Inverse)（一个增长速率非常接近于零的函数）。

## 解决方案

如果已经知道并查集这种数据结构，那么本题将很容易解决：

从小到大枚举每个质数$p$，并且通过$p$直接枚举出如题意所需要的改变一位的质数$p'$，合并质数$p$和$p'$的所在集合。合并完成后，最终判断$p$和$2$是否在同一集合即可。

## 代码

```C++
# include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N=1e7;
int pr[N/10+100],m=0;
bool vis[N+4];
int fa[N+4];
int find(int x){return fa[x]==x?x:fa[x]=find(fa[x]);}
void merge(int x,int y){fa[find(x)]=find(y);}
vector<int>pw10;
int now[1004],p=0;
void gen(int u){
    p=0;
    vector<int>d;
    for(int x=u;x;x/=10)
        d.push_back(x%10);
    for(int i=0;i<d.size();i++){
        int x=u-pw10[i]*d[i];
        if(i+1==d.size()) x+=pw10[i];
        for(int j=(i+1==d.size()?1:0);j<d[i];j++){
            now[++p]=x;
            x+=pw10[i];
        }
    }
    if(d.size()>=2&&d[d.size()-2]!=0)
        now[++p]=u-pw10[d.size()-1]*d.back();
}
int main(){
    vis[1]=1;
    for(int i=2;i<=N;i++)
        if(!vis[i]){
            pr[++m]=i;
            for(ll j=1ll*i*i;j<=N;j+=i)
                vis[j]=1;
        }
    pw10.push_back(1);
    while(pw10.back()<=N) pw10.push_back(pw10.back()*10);
    for(int i=1;i<=m;i++)
        fa[pr[i]]=pr[i];
    ll ans=0;
    for(int i=1;i<=m;i++){
        int u=pr[i];
        gen(u);
        for(int i=1;i<=p;i++){
            int k=now[i];
            if(vis[k]) continue;
            merge(k,u);
        }
        if(find(2)!=find(u)) ans+=u;
    }
    printf("%lld\n",ans);
}

```
