---
title: Project Euler 186
category:
  - Project Euler
tags:
  - 并查集
mathjax: true
date: 2022-05-19 21:57:01
---

<escape><!-- more --></escape>

# Project Euler 186

## 题目

### Connectedness of a network

Here are the records from a busy telephone system with one million users:

|Rec Nr|Caller|Called|
|-|-|-|
|$1$|$200007$|$100053$|
|$2$|$600183$|$500439$|
|$3$|$600863$|$701497$|
|$\dots$|$\dots$|$\dots$|

The telephone number of the caller and the called number in record $n$ are $\text{Caller}(n) = S_{2n-1}$ and $\text{Called}(n) = S_{2n}$ where $S_{1,2,3,\dots}$ come from the “Lagged Fibonacci Generator”:

For $1 \le k \le 55, S_k = [100003 - 200003k + 300007 k^3] (\text{modulo\ } 1000000)$<br>
For $56 \le k, S_k = [S_k-24 + S_k-55] (\text{modulo\ } 1000000)$

If $\text{Caller(n)} = \text{Called(n)}$ then the user is assumed to have misdialled and the call fails; otherwise the call is successful.

From the start of the records, we say that any pair of users $X$ and $Y$ are friends if $X$ calls $Y$ or vice-versa. Similarly, $X$ is a friend of a friend of $Z$ if $X$ is a friend of $Y$ and $Y$ is a friend of $Z$; and so on for longer chains.

The Prime Minister’s phone number is $524287$. After how many successful calls, not counting misdials, will $99\%$ of the users (including the PM) be a friend, or a friend of a friend etc., of the Prime Minister?

## 并查集

[并查集](https://en.wikipedia.org/wiki/Disjoint-set_data_structure)：用于高效处理一些不相交集合的数据结构。一般有两个操作：合并两个集合；查询两个元素是否在同一个集合中。

可以通过优化将并查集这两种单次操作优化到$O(\alpha(n))$级别，其中$\alpha(n)$是[反阿克曼函数](https://en.wikipedia.org/wiki/Ackermann_function#Inverse)（一个增长速率非常接近于零的函数）。

## 解决方案

本题为并查集的模板题，直接用并查集数据结构实现。

代码中需要维护每个集合的大小。为了避免错误，只有两个元素不属于同一个集合时才需要合并。

## 代码

```C++
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N=1000000,P=524287,A=N/100*99;
const int M=N*5;
int fa[N],sz[N];
int find(int x){return x==fa[x]?x:fa[x]=find(fa[x]);}
void merge(int x,int y){
    int u=find(x),v=find(y);
    if(u!=v){
        fa[u]=v;
        sz[v]+=sz[u];
    }
}
int s[M];
int main(){
    int cnt=0,ans=0;
    for(int i=0;i<N;i++)
        fa[i]=i,sz[i]=1;
    for(int i=1;i<=55;i++)
        s[i]= (1ll * 300007 * i * i * i + 100003 - 200003 * i) % N;
    for(int i=56;i<M;i++)
        s[i]= (s[i - 24] + s[i - 55]) % N;
    for(int i=2;i<M;i+=2){
        if(s[i] == s[i - 1]) ++cnt;
        else{
            merge(s[i], s[i - 1]);
            if(sz[find(P)]>=A){
                ans=i/2-cnt;
                break;
            }
        }
    }
    printf("%d\n",ans);
}
```
