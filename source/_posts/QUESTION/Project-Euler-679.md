---
title: Project Euler 679
tags:
  - Project Euler
  - AC自动机
  - 动态规划
mathjax: true
date: 2022-07-27 23:50:02
---

<escape><!-- more --></escape>

# Project Euler 679

## 题目

### Freefarea

Let $S$ be the set consisting of the four letters $\{\texttt{`A'},\texttt{`E'},\texttt{`F'},\texttt{`R'}\}$.

For $n\ge 0$, let $S^*(n)$ denote the set of words of length $n$ consisting of letters belonging to $S$.

We designate the words $\texttt{FREE}, \texttt{FARE}, \texttt{AREA}, \texttt{REEF}$ as <i>keywords</i>.

Let $f(n)$ be the number of words in $S^*(n)$ that contains all four keywords exactly once.

This first happens for $n=9$, and indeed there is a unique 9 lettered word that contain each of the keywords once: $\texttt{FREEFAREA}$
So, $f(9)=1$.

You are also given that $f(15)=72863$.

Find $f(30)$.

## 解决方案

先将这$D=4$个关键字插入一棵[Trie树](https://en.wikipedia.org/wiki/Trie)，然后再使用[AC自动机](https://en.wikipedia.org/wiki/Aho%E2%80%93Corasick_algorithm)算法将这棵Trie树构建成一个[确定有限状态自动机(DFA)](https://en.wikipedia.org/wiki/Deterministic_finite_automaton)。这个自动机每次读入一个字符，就会从当前状态转移到下一个指定的状态。一开始构建的Trie树的$D$个字符串的最终节点分别作为$D$个字符串的接受状态。也就是说，在构建Trie树时，假设插入一个字符串$s$后，最终到达的节点的编号（状态）为$st$，那么现在逐渐读入一个新的字符串$t$，并按照给定的转移过程逐渐转移，最终到达了状态$m$，那么相当于当前读入了一个字符串$s$。

构建出DFA后，那么现在就将问题变成了一个图$G=(V,E)$上的动态规划问题，整个图一共有$|V|$个节点，编号$0\sim |V|-1$。假设$D$个接受状态分别为$s_0,s_1,\dots,s_{D-1}$。

由于题目中要求$D$个字符串都需要恰好每个字符串都包含一次，因此考虑用一个$D$位二进制数$d=d_{D-1}d_{D-2}\dots d_0$来表示图上的路径中，节点$s_0,s_1,\dots,s_{D-1}$节点经过情况。如果$s_k$被路径经过，那么$d_k=1$，否则$d_k=0$。

令$N=30$。令状态$g(i,j,k)(0\le i\le N,0\le j<|V|,0\le k<2^D)$表示有多少条从节点$0$开始的长度为$i$的路径中，目前在节点$j$，并且经过的接受状态节点情况为$k$。那么考虑使用我为人人式的方法进行如下实现：

对于节点$j$的每个后继节点$v$：

如果$v$是某个接受接受状态节点$s_l$，并且$2^l\&k=0$，那么就有转移$g(i,j,k)\rightarrow g(i+1,v,2^l|k)$。

如果$v$不是接受状态节点，那么就有转移$g(i,j,k)\rightarrow g(i+1,v,k)$。

那么最终结果为：

$$f(N)=\sum_{j=0}^{|V|-1}g(N,j,2^D-1)$$

## 代码

```C++
#include <bits/stdc++.h>
typedef long long ll;
using namespace std;
const int N=30;
const int MX=1004;
const int D=4;
string S="AEFR";
vector<string>key_word{
    "FREE",
    "FARE",
    "AREA",
    "REEF"
};
unordered_map<char,int>tr[MX];
int fail[MX];
int pos[MX];
int tot=0;
void add(int id,string &s){
    int p=0;
    for(char ch:s){
        if(!tr[p].count(ch)) tr[p][ch]=++tot;
        p=tr[p][ch];
    }
    pos[p]=id;
}
void build(){
    queue<int>q;
    for(char ch:S)
        if(tr[0].count(ch)) q.push(tr[0][ch]);
    while(!q.empty()){
        int u=q.front();q.pop();
        for(char ch:S){
            if(tr[u].count(ch)) fail[tr[u][ch]]=tr[fail[u]][ch],q.push(tr[u][ch]);
            else tr[u][ch]=tr[fail[u]][ch];
        }
    }
}
ll f[N][MX][1<<D];
int main(){
    memset(pos,-1,sizeof(pos));
    for(int i=0;i<key_word.size();i++)
        add(i,key_word[i]);
    build();
    f[0][0][0]=1;
    for(int i=0;i<N;i++)
        for(int j=0;j<=tot;j++)
            for(int k=0;k<(1<<D);k++)
                for(auto &[ch,v]:tr[j]){
                    int st=k;
                    if(pos[v]!=-1){
                        if(k>>pos[v]&1) continue;
                        st|=1<<pos[v];
                    }
                    f[i+1][v][st]+=f[i][j][k];
                }
    ll ans=0;
    for(int j=0;j<=tot;j++)
        ans+=f[N][j][(1<<D)-1];
    printf("%lld\n",ans);
}

```
