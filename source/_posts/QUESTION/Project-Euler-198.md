---
title: Project Euler 198
category:
  - Project Euler
tags:
mathjax: true
date: 2022-05-24 11:02:17
---

<escape><!-- more --></escape>

# Project Euler 198

## 题目

### Ambiguous Numbers

A best approximation to a real number $x$ for the denominator bound $d$ is a rational number $\dfrac{r}{s}$ (in reduced form) with $s \le d$, so that any rational number $\dfrac{p}{q}$ which is closer to $x$ than $\dfrac{r}{s}$ has $q > d$.

Usually the best approximation to a real number is uniquely determined for all denominator bounds. However, there are some exceptions, e.g. $\dfrac{9}{40}$ has the two best approximations $\dfrac{1}{4}$ and $\dfrac{1}{5}$ for the denominator bound $6$. We shall call a real number $x$ *ambiguous*, if there is at least one denominator bound for which $x$ possesses two best approximations. Clearly, an ambiguous number is necessarily rational.

How many ambiguous numbers $x=\dfrac{p}{q}$, $0 < x < \dfrac{1}{100}$, are there whose denominator $q$ does not exceed $10^8$?

## 解决方案

如果存在一个正整数$m$，使得两个分数$x=\dfrac{a}{c},y=\dfrac{b}{d}$在第$m$个Farey序列是相邻的。那么$\dfrac{x+y}{2}$很明显是一个答案。

因此，可以考虑对[Stern-Brocot Tree](https://en.wikipedia.org/wiki/Stern%E2%80%93Brocot_tree)进行遍历，枚举出Farey序列中有可能在Farey序列中相邻的分数，并统计。

令$R=100$。为了减少枚举量，对于枚举出的两个分数$x,y$，如果$x\ge\dfrac{1}{R}$，那么没有必要在这个区间上继续寻找答案（此时这里计算出来的$\dfrac{x+y}{2}$都大于$\dfrac{1}{R}$，不合题意）。

另外，由于直接使用递归会造成栈溢出（分析代码不难知道，最大的递归深度将会达到$O(N)$级别），因此这里使用非递归的方式遍历Stern-Brocot Tree.

## 代码

```C++
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const ll N=100000000;
const int R=100;
struct S{
    ll a,c,b,d;
};
int main(){
    int ans=0,cnt=0;
    stack<S>st;
    st.push(S{0,1,1,1});
    while(!st.empty()){
        S s=st.top();st.pop();
        ll a=s.a,b=s.b,c=s.c,d=s.d;
        if(c*d*2>N) continue;
        // 左边的分数已经大于等于1/R，没必要取下去。
        if(a*R>=c) continue;
        ll p=a+b,q=c+d;
        ll u=a*d+b*c,v=c*d*2;
        if(u*R<v) ++ans;
        else ++cnt;
        st.push(S{a,c,p,q});
        st.push(S{p,q,b,d});
    }
    printf("%d %d\n",cnt,ans);
}

```
