---
title: Project Euler 149
tags:
  - Project Euler
  - 动态规划
mathjax: true
date: 2022-05-15 10:16:07
---

<escape><!-- more --></escape>

# Project Euler 149

## 题目

### Searching for a maximum-sum subsequence

Looking at the table below, it is easy to verify that the maximum possible sum of adjacent numbers in any direction (horizontal, vertical, diagonal or anti-diagonal) is $16 (= 8 + 7 + 1)$.

|||||
|-|-|-|-|
|$-2$|$5$|$3$|$2$|
|$9$|$-6$|$5$|$1$|
|$3$|$2$|$7$|$3$|
|$-1$|$8$|$-4$|$8$|

Now, let us repeat the search, but on a much larger scale:

First, generate four million pseudo-random numbers using a specific form of what is known as a “Lagged Fibonacci Generator”:

For $1 \leq k \leq 55, s_k = [100003 - 200003k + 300007k^3] (\mathrm{modulo\ } 1000000) - 500000$

For $56 \leq k \leq 4000000$, $s_k = [s_{k-24} + s_{k-55} + 1000000] (\mathrm{modulo\ } 1000000) - 500000$.

Thus, $s_{10} = -393027$ and $s_{100} = 86613$.

The terms of $s$ are then arranged in a $2000\times2000$ table, using the first $2000$ numbers to fill the first row (sequentially), the next $2000$ numbers to fill the second row, and so on.

Finally, find the greatest sum of (any number of) adjacent entries in any direction (horizontal, vertical, diagonal or anti-diagonal).

## 解决方案

需要将表格按照同行，同列，同主副对角线下，预处理一个个数组，方便求相邻之和。

对于每一个数组$a$（其中设$m$为其长度），视为整个问题中的一个个独立的子问题。用动态规划求这些子问题的最大子段和。

设$f(i)(1\le i\le m)$为以数组第$i$个元素为结尾的所有子段的最大和，那么可以列出如下状态转移方程：

$$
f(i)=
\left \{\begin{aligned}
  &a[i]  & & \mathrm{if\quad} i=1 \\
  &\max(a[i],f(i-1)+a[i]) & & \mathrm{else}
\end{aligned}\right.
$$

其中，最后一行两种决策分别是：要么将这个元素拼接到前面$f(i-1)$的子段末尾，要么独立自乘一个子段。

答案为$\max_{i=1}^m f(i)$。

所有子问题的答案的最大值即为问题答案。

## 代码

```C++
# include <bits/stdc++.h>
using namespace std;
const int N=2000;
const int m=500000;
int s[N*N+4];
vector<int>a[N],b[N],g[N+N],h[N+N];
int solve(vector<int>&v){
    int mx=0,s=0;
    for(int x:v){
        if(s<0) s=x;
        else s+=x;
        mx=max(mx,s);
    }
    return mx;
}
int main(){
    for(int k=1;k<=N*N;k++){
        if(k<=55) s[k]=(300007ll*k*k*k-200003*k+100003)%(m*2)-m;
        else s[k]=(s[k-24]+s[k-55]+m*2)%(m*2)-m;
    }
    for(int i=0,p=1;i<N;i++){
        for(int j=0;j<N;j++,p++){
            a[i].push_back(s[p]);
            b[j].push_back(s[p]);
            g[i+j].push_back(s[p]);
            h[i-j+N-1].push_back(s[p]);
        }
    }
    int ans=0;
    for(int i=0;i<N;i++)
        ans=max(ans,max(solve(a[i]),solve(b[i])));
    for(int i=0;i<2*N-1;i++)
        ans=max(ans,max(solve(g[i]),solve(h[i])));
    printf("%d\n",ans);
}

```
