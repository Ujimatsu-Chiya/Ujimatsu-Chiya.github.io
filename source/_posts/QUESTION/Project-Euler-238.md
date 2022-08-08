---
title: Project Euler 238
category:
  - Project Euler
tags:
  - 双指针
mathjax: true
date: 2022-07-04 18:02:20
---

<escape><!-- more --></escape>

# Project Euler 238

## 题目

### Infinite string tour

Create a sequence of numbers using the “Blum Blum Shub” pseudo-random number generator:

$\begin{aligned}
s_0&=14025256\\
s_{n+1}&=s_n^2 \mod 20300713
\end{aligned}$

Concatenate these numbers  $s_0s_1s_2\dots$ to create a string $w$ of infinite length.

Then, $w = \color{blue}14025256741014958470038053646\dots$

For a positive integer $k$, if no substring of $w$ exists with a sum of digits equal to $k$, $p(k)$ is defined to be zero. If at least one substring of $w$ exists with a sum of digits equal to $k$, we define $p(k) = z$, where $z$ is the starting position of the earliest such substring.

For instance:

The substrings $\color{blue}1, 14, 1402, \dots$ with respective sums of digits equal to $1, 5, 7, \dots$

start at position $\mathbf{1}$, hence $p(1) = p(5) = p(7) = \dots = \mathbf{1}$.

The substrings $\color{blue}4, 402, 4025, \dots$
with respective sums of digits equal to $4, 6, 11, \dots$

start at position $\mathbf{2}$, hence $p(4) = p(6) = p(11) = \dots = 2$.

The substrings $\color{blue} 02, 0252, \dots$
with respective sums of digits equal to $2, 9, \dots$

start at position $\mathbf{3}$, hence $p(2) = p(9) = \dots = \mathbf{3}$.

Note that substring $\color{blue}025$ starting at position $3$, has a sum of digits equal to $7$, but there was an earlier substring (starting at position $1$) with a sum of digits equal to $7$, so $p(7) = 1$, not $3$.

We can verify that, for $0 < k \le 10^3, \sum p(k) = 4742$. Find $\sum p(k)$, for $0 < k \le 2\cdot10^{15}$.

## 解决方案

不难发现，序列$s$是一个周期序列，其周期为$2534198$.

因此，字符串$w$必定也是一个周期序列。$w$的字符串周期为$t=18886117$。单个周期中，所有数之和为$T=80846691$.因此有$p(k)=p(k+T)$，因此这里只需要求出所有$1\le k\le T$的$p(k)$值即可。

本方案通过暴力枚举的方式直接找到这一部分的$p$值，时间复杂度为$O(t^2)$。

为了压缩时间，考虑以下缩减时间复杂度的方法：在枚举起点的时候，如果发现对于某个值$s$，$p(s+1),p(s+2),\dots,p(T)$都已经求解出来，那么在枚举区间右端点$r$时，保持$\sum_{i=l}^r w_i\le s$。每次枚举$i$时，都先要将$s$维护好。经过测试，这种方式让外层循环进行了不到$100$次，效率可以接受。

对于某个$k$，计算出$p(k)$后，那么就需要计算$1\sim N$中有多少个值和$k$关于模$T$同余。这个值不难计算出是$\lfloor \dfrac{N}{T}\rfloor+[k\neq T \wedge k\le n\%T]$,其中$[]$是示性函数。

需要注意的是，有一部分$p$值，以$p(k)$为起点，$k$为和值的字符串跨越了两个周期，本代码给第二个区间预留了$C=100$位数字。

对于

## 代码

```C++
# include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const ll N=2e15;
int s0 = 14025256;
int mod = 20300713;
const int A=2e7+1004,B=9e7+4,C=100;
int d[A+C],t=0,T=0;
bool vis[B+C];
int main(){
    int pre=t;
    for(int s=s0;;){
        for(int x=s;x;d[++t]=x%10,T+=d[t],x/=10);
        reverse(d+pre+1,d+t+1);
        pre=t;
        s=1ll*s*s%mod;
        if(s==s0) break;
    }
    int rs=T;
    for(int i=1;i<=C;i++)
        d[t+i]=d[i],rs+=d[i];
    ll ans=0;
    for(int l=1,ps=T;l<=t+C;l++){
        if(l>1&&d[l-1]==0) continue;
        // 关键代码，大于$ps$的那一部分不需要再枚举。
        ps=min(ps,rs);
        for(;ps>0&&vis[ps];ps--);
        if(ps==0) break;
        for(int r=l,s=0;r<=t+C&&s+d[r]<=ps;r++){
            s+=d[r];
            if(s>0&&!vis[s]){
                ll cnt=N/T+(s==T?0:s<=N%T);
                ans+=cnt*l;
                vis[s]=true;
            }
        }
        rs-=d[l];
    }
    printf("%lld\n",ans);
}

```
