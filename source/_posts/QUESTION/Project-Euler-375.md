---
title: Project Euler 375
tags:
  - Project Euler
mathjax: true
date: 2022-07-12 00:17:19
---

<escape><!-- more --></escape>

# Project Euler 375

## 题目

### Minimum of subsequences

Let $S_n$ be an integer sequence produced with the following pseudo-random number generator:
$$
\begin{aligned}
S_0  &= 290797 \\
S_{n+1}  &= S_n^2 \mod 50515093
\end{aligned}
$$

Let $A(i, j)$ be the minimum of the numbers $S_i, S_{i+1}, \ldots, S_j$ for $i\le j$.

Let $M(N) = \sum A(i, j)$ for $1 \le i \le j \le N$.

We can verify that $M(10) = 432256955$ and $M(10\,000) = 3264567774119$.

Find $M(2\,000\,000\,000)$.

## 单调栈

单调栈是一种数据结构，栈内元素保证单调性。这种数据结构用于维护这个序列中，每一个数在左边/右边比它大/小的第一个数。

如果要求某个数右边比它第一个大的数，那么考虑从右往左遍历序列。对于每一个数，弹出栈中比它小的所有数。如果栈未空，那么栈顶的数就是答案，否则说明这个数右边没有比它大的数。最终把自身压入这个栈中。

## 解决方案

注意到，$S$是一个周期序列，其周期$T=6308948$，最小值为$m=3$.

对于这道题，我们考虑这个序列中每一个数$S_i$能够对答案$M(N)$。这启发我们先使用单调栈找出每一个数$S_i$分别在左边和右边严格比它小的第一个数$S_l,S_r$。那么对于所有区间$[i,j],l < i\le j< r$，区间$[i,j]$都是以$S_i$为最小值，这些区间一共有$(r-i)\cdot (i-l)$个。另外，注意到$S$是周期序列，因此对$S_{i+T}$而言，也会有同样类似的结论。

如果最小值$m$是某个区间的贡献，那么$m$可能横跨多个区间。为了避免重复计算，接下来先考虑比$m$大的数的贡献。

接下来我们将原序列$S$中的$N$个值分成三部分，分别是：$S$的前$T$个数，$S$的最后$T$个数，以及中间其它数。由于$S$有周期性，我们只考虑$S$的前$2T+N\%T$项，对这些项使用上面提到的单调栈算法两次，分别求出两个关于$i$的序列$l[i],r[i]$。不难发现可以将这些$i-l[i],r[i]-i$的值对应到原式序列的一个个下标里面。

因此对前$T$个数和后$T$个数分别独立计算求和。对于中间剩下的$N-2T$这一部分数，可以考虑将它分成每$T$个元素一块，整体计算贡献。

在计算的过程中统计所有非最小值的区间贡献数量之和。长度为$N$的序列意味着有$\dfrac{N(N+1)}{2}$个区间，那么最后求$m$的时候用$\dfrac{N(N+1)}{2}$减去这些区间数量和，那么就得到了$m$的区间贡献数。

## 代码

```C++
#include <bits/stdc++.h>
typedef long long ll;
using namespace std;
int Q=2e9,T;
const int A=290797,M=50515093;
//容易知道，S1到后面为一个循环数组，其中周期为T。
int S[M*3];
int l[M*3],r[M*3];
void gen(int m){
    stack<int>st;
    for(int i=0;i<m;i++){
        while(!st.empty() && S[i] < S[st.top()])
            st.pop();
        if(st.empty()) l[i]=0;
        else l[i]=st.top()+1;
        st.push(i);
    }
    while(!st.empty())
        st.pop();
    for(int i=m-1;i>=0;i--){
        while(!st.empty() && S[i] < S[st.top()])
            st.pop();
        if(st.empty()) r[i]=m-1;
        else r[i]=st.top()-1;
        st.push(i);
    }
}
ll solve(){
    //由于S数组是一个循环数组，故分类处理。
    int mn=*min_element(S, S + T);
    ll res=1ll*Q*(Q+1)/2,ans=0;
    if(Q<=T*2){
        for(int i=T;i<Q;i++)
            S[i]=S[i-T];
        gen(Q);
        for(int i=0;i<Q;i++){
            ll tp=1ll*(i-l[i]+1)*(r[i]-i+1);
            ans+=tp*S[i];
            res-=tp;
        }
        ans+=res*mn;
    }
    else{
        for(int i=0;i<T;i++)
            S[i+T]=S[i+T+T]=S[i];
        int block=Q/T,rest=Q%T;
        gen(2*T+rest);
        for(int i=0;i<T;i++){
            ll tp=1ll*(i-l[i]+1)*(r[i]-i+1);
            ans+=tp*S[i];
            res-=tp;
            int j=2*T+rest-1-i;
            tp=1ll*(j-l[j]+1)*(r[j]-j+1);
            ans+=tp*S[j];
            res-=tp;
            tp=1ll*(i+T-l[i+T]+1)*(r[i]-i+1);
            ll c=block-2+(i<rest);
            ans+=tp*S[i]*c;
            res-=tp*c;
        }
        ans+=res*mn;
    }
    return ans;
}
int main(){
    S[0]=1ll*A*A%M;
    for(int i=1;i<M;i++){
        S[i]=1ll*S[i-1]*S[i-1]%M;
        if(S[i]==S[0]){
            T=i;break;
        }
    }
    printf("%lld\n",solve());
}
```
