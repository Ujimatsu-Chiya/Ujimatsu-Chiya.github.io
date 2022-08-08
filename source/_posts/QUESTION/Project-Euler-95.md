---
title: Project Euler 95
category:
  - Project Euler
tags:
mathjax: true
date: 2022-05-02 16:37:23
---

<escape><!-- more --></escape>

# Project Euler 95

## 题目

### Amicable chains

The proper divisors of a number are all the divisors excluding the number itself. For example, the proper divisors of $28$ are $1, 2, 4, 7$, and $14$. As the sum of these divisors is equal to $28$, we call it a perfect number.

Interestingly the sum of the proper divisors of $220$ is $284$ and the sum of the proper divisors of $284$ is $220$, forming a chain of two numbers. For this reason, $220$ and $284$ are called an amicable pair.

Perhaps less well known are longer chains. For example, starting with $12496$, we form a chain of five numbers:

$$ 12496 \rightarrow 14288 \rightarrow 15472 \rightarrow 14536 \rightarrow 14264 (\rightarrow 12496 \rightarrow \dots)$$

Since this chain returns to its starting point, it is called an amicable chain.

Find the smallest member of the longest amicable chain with no element exceeding one million.

## 解决方案

将$1\sim N$中所有数的真因数和通过筛法计算出来，这需要$O(N\log N)$的时间。

从图论的角度上看，这是一张所有节点都只有一条出边的有向图（每个节点$i$向其真因数和的节点$\mathrm{sigma}[i]$连边），因此每个节点最多只属于一个环。

因此本问题就变成了在这个特殊的图上找出那个最大的环。

如果一个数的真因数和大于$N$，那么根据题意，将这个节点标记为无效节点（答案肯定不是这个节点的值）。可以递归地发现：如果一个节点的后继为无效节点，那么这个节点本身就是无效节点。

此外，在枚举的过程中，还需要判断这个节点是否为链上，而不是在环上。

本代码也使用了记忆化搜索，用来记录这些节点的状态值是无效的，在环上的长度，还是在链上。

## 代码

```C++
# include <bits/stdc++.h>
using namespace std;
const int N=1000000;
//f：记录答案，sigma：真因数之和，st：深搜时用来存放节点的栈，pos：节点在栈中的位置。
int f[N+4],sigma[N + 4],pos[N + 4];
int st[N+4];
int dfs(int u,int fl){
    if(f[u]) return f[u];
    st[fl]=u;
    //如果这个节点已经在栈中了，那么说明找到了一个环，该节点及栈中以后的节点都在这个环中。
    if(pos[u]){
        for(int i=pos[u];i<fl;i++)
            f[st[i]]=fl-pos[u];
        return f[u];
    }
    pos[u]=fl;
    //三种情况：无效节点，后继节点是无效节点，本节点是链上的节点。
    if(sigma[u] == 0 || dfs(sigma[u], fl + 1) == -1 || f[u] == 0) return f[u]=-1;
    pos[u]=0;
    return f[u];
}
int main(){
    for(int i=1;i<=N;i++)
        for(int j=i+i;j<=N;j+=i)
            sigma[j]+=i;
    for(int i=1;i<=N;i++)
        if(sigma[i] > N) sigma[i]=0;
    int mx=0,ans=0;
    for(int i=1;i<=N;i++){
        if(dfs(i,1)>mx){
            mx=f[i];
            ans=i;
        }
    }
    printf("%d\n",ans);
}

```
