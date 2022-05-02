---
title: Project Euler 92
tags:
  - Project Euler
mathjax: true
date: 2022-05-02 16:37:12
---

<escape><!-- more --></escape>

# Project Euler 92

## 题目

### Square digit chains

A number chain is created by continuously adding the square of the digits in a number to form a new number until it has been seen before.

For example,

$44 \rightarrow 32 \rightarrow 13 \rightarrow 10 \rightarrow \mathbf{1} \rightarrow \mathbf{1}$
$85 \rightarrow \mathbf{89}  \rightarrow 145 \rightarrow 42 \rightarrow 20 \rightarrow 4 \rightarrow 16 \rightarrow 37 \rightarrow 58 \rightarrow \mathbf{89}$

Therefore any chain that arrives at $1$ or $89$ will become stuck in an endless loop. What is most amazing is that EVERY starting number will eventually arrive at $1$ or $89$.

How many starting numbers below ten million will arrive at $89$?

## 解决方案

本代码使用递归的方式。通过直接计算数位平方和恶，判断每一个数属于$1$的类还是$89$的类。

采用记忆化递归的方式，将每个值的计算结果存好，减少计算时间，保证每个数只被计算一次。

## 代码

```C++
# include <bits/stdc++.h>
using namespace std;
const int M=10000000;
char f[max(M,300)+4];
char dfs(int u){
    if(u==1) return 1;
    else if(u==89) return 0;
    else if(f[u]!=-1) return f[u];
    int s=0;
    for(int w=u;w;w/=10)
        s+=(w%10)*(w%10);
    return f[u]=dfs(s);
}
int main(){
    memset(f,-1,sizeof(f));
    int ans=0;
    for(int i=1;i<=M;i++){
        if(dfs(i)==0) ++ans;
    }
    printf("%d\n",ans);
}

```
