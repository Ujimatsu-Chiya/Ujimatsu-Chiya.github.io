---
title: Project Euler 303
category:
  - Project Euler
tags:
mathjax: true
date: 2022-07-06 13:08:33
---

<escape><!-- more --></escape>

# Project Euler 303

## 题目

### Multiples with small digits

For a positive integer $n$, define $f(n)$ as the least positive multiple of $n$ that, written in base $10$, uses only digits $\le 2$.

Thus $f(2)=2, f(3)=12, f(7)=21, f(42)=210, f(89)=1121222$.

Also, $\sum^{100}_{n=1}\dfrac{f(n)}{n}=11363107$.

Find $\sum^{10000}_{n=1}\dfrac{f(n)}{n}$.

## 解决方案

对于每个询问的$1\le n\le N$，其中$N=10000$。考虑从小到大枚举所有数。广度优先搜索可以帮助我们高效枚举，并且能够进行适当的剪枝。

根据广度优先搜素的性质，搜索的数恰好是从小到大的。当前搜索到一个数$m$，那么就可以考虑往它的后面分别添加三个数$0,1,2$，从而扩展出新的$3$个数$10m,10m+1,10m+2$。

找到一个最小的满足条件的数位$n$的倍数，本质上是找到一个最小的满足条件的数，其模$n$为$0$，因此从模的角度思考。广度优先搜索剪枝的地方在于，如果$(10m+i)\%n$已经出现过，那么就不需要再将$10m+i$这个数放进队列中。因为由它继续扩展出来的数，模$n$的结果也将和往常一样。

最终找到一个模$n$为$0$的数即为答案，单次询问的时间复杂度为$O(n)$.

## 代码

```C++
# include <bits/stdc++.h>
using namespace std;
typedef unsigned long long ull;
const int N=10000;
bool vis[N+4];
ull solve(int n)
{
    if(n<=2) return 1;
    memset(vis,0,sizeof(vis));
    queue<ull>q;
    q.push(1);q.push(2);
    vis[1]=vis[2]=1;
    while (1) {
        ull x=q.front();q.pop();
        if (x%n==0) return x/n;
        for (unsigned i=0;i<=2;i++) {
            ull y=x*10+i;
            if (!vis[y%n]) {
                vis[y%n] = 1;
                q.push(y);
            }
        }
    }
}
int main(){
    ull ans=0;
    for(int i=1;i<=N;i++)
        ans+=solve(i);
    printf("%llu\n",ans);
}

```
