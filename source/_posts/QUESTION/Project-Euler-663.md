---
title: Project Euler 663
tags:
  - Project Euler
  - 线段树
mathjax: true
date: 2022-07-27 23:49:44
---

<escape><!-- more --></escape>

# Project Euler 663

## 题目

### Sums of subarrays

Let $t_k$ be the **tribonacci numbers** defined as:

$\begin{aligned}
&\quad t_0 = t_1 = 0;\\
&\quad t_2 = 1; \\
&\quad t_k = t_{k-1} + t_{k-2} + t_{k-3} \quad \text{   for   }  k \ge 3
\end{aligned}$

For a given integer $n$, let $A_n$ be an array of length $n$ (indexed from $0$ to $n-1$), that is initially filled with zeros.

The array is changed iteratively by replacing $A_n[(t_{2 i-2} \text{ mod } n)]$ with $A_n[(t_{2 i-2} \text{ mod } n)]+2 (t_{2 i-1} \text{ mod } n)-n+1$ in each step $i$.

After each step $i$, define $M_n(i)$ to be $\displaystyle \max\{\sum_{j=p}^q A_n[j]: 0\le p\le q<n\}$, the maximal sum of any contiguous subarray of $A_n$.

The first 6 steps for $n=5$ are illustrated below:

Initial state: $\, A_5=\{0,0,0,0,0\}$

Step $1:\quad \Rightarrow A_5=\{-4,0,0,0,0\}$ , $M_5(1)=0$

Step $2:\quad \Rightarrow A_5=\{-4, -2, 0, 0, 0\}$ , $M_5(2)=0$

Step $3:\quad \Rightarrow A_5=\{-4, -2, 4, 0, 0\}$ , $M_5(3)=4$

Step $4:\quad \Rightarrow A_5=\{-4, -2, 6, 0, 0\}$ , $M_5(4)=6$

Step $5:\quad \Rightarrow A_5=\{-4, -2, 6, 0, 4\}$ , $M_5(5)=10$

Step $6:\quad \Rightarrow A_5=\{-4, 2, 6, 0, 4\}$ , $M_5(6)=12$

Let $\displaystyle S(n,l)=\sum_{i=1}^l M_n(i)$. Thus $S(5,6)=32$.

You are given $S(5,100)=2416$, $S(14,100)=3881$ and $S(107,1000)=1618572$.

Find $S(10\,000\,003,10\,200\,000)-S(10\,000\,003,10\,000\,000)$.

## 线段树

[线段树](https://en.wikipedia.org/wiki/Segment_tree)是一种用于维护区间内的数的一些计算结果，这些计算需要满足**结合律**（如加法，乘法，最小值，最大值）。假设这个序列为$a$，长度为$L$。它有以下特点：

- 树的每个节点都代表一个区间的统计结果。
- 根节点代表着整个区间$[1,L]$，每个叶节点代表着某一个长度为$1$的区间$[i,i]$。
- 如果当前节点代表的区间为$[L,R]$，那么左子节点代表的区间是$[L,M]$，右子节点是$[M+1,R]$，其中$M=\lfloor\dfrac{L+R}{2}\rfloor$。

线段树的三个操作：

1. 建树（初始化）。给定一个序列，自底向上地建立出一颗线段树。当两个子节点的信息维护好时，当前节点的信息也能迅速维护好。单次操作仅需要$O(L)$的时间复杂度。建树一旦完成，以后就不需要进行操作了。
2. 修改。从根节点往下搜索，递归找到需要修改的**整个**区间。修改完成后，再自底向上更新所有祖先节点的信息。单次操作仅需要$O(\log L)$的时间复杂度。
3. 查询。从根节点往下搜索，如果查询的区间覆盖了当前整个区间，那么直接返回当前节点的信息；如果查询的区间和左/右子节点有交集，那么递归查询后，将结果合并。最终向上传递。单次操作也仅需要$O(\log L)$的时间复杂度。

因此，维护好各个节点，可以以高效的方式维护出需要结果的值。

## 解决方案

考虑使用线段树解决本题。每个节点$p$所代表的区间$[L,R]$需要维护四个信息：

|||
|-|-|
|$\text{dat}$|$\max_{L\le l\le r\le R} \sum_{i=l}^r a[i]$，也就是题目中所需要求的值|
|$\text{lmax}$|$\max_{L\le k\le R} \sum_{i=L}^k a[i]$，也就是最大前缀和|
|$\text{rmax}$|$\max_{L\le k\le R} \sum_{i=k}^R a[i]$，也就是最大后缀和|
|$\text{sum}$|$\sum_{i=L}^R a[i]$，也就是区间内的所有数之和|

那么，假设$p$的左右子节点分别为$ls,rs$，那么这四个属性的自低向上维护方式为：

|||
|-|-|
|$p.\text{dat}=\max(ls.\text{dat},rs.\text{dat},ls.\text{rmax}+rs.\text{lmax})$|这说明当前区间的答案要么是取自左子节点，要么是取自右子节点；要么是左子节点的最大后缀进和与右子节点的最大前缀和合并形成一个新的答案。
|$p.\text{lmax}=\max(ls.\text{lmax},ls.\text{sum}+rs.\text{lmax})$|这说明当前区间的最大前缀和要么是来自左子节点的最大前缀和，要么是左子节点的整个区间和右子节点的最大前缀和合并形成当前区间的前缀。|
|$p.\text{rmax}=\max(rs.\text{rmax},rs.\text{sum}+ls.\text{rmax})$|与最大前缀和类似。|
|$p.\text{sum}=ls.\text{sum}+rs.\text{sum}$||

其它仅需要遵循线段树的模式即可。

## 代码

第一份代码，严格在线段树上执行了计算$S(n,l)$时的各种操作，包括一开始建树，并且每次更新后计算所需要的结果。时间复杂度为$O(n\log l)$。并且执行了两次，效率非常低。

第二份代码，则减少了一部分没有必要的工作。由于计算的$n$相同，并且前$10000000$次操作的结果都被减去了。那么我们一开始先不建树，等前$10000000$次修改完成了，再建树。由于这个时候是直接对序列进行修改，时间复杂度为$O(1)$，忽略不计。建树完成后，再进行$200000$次的询问和记录答案操作。总体时间复杂度为$O(l+(l-n)\log l)$。

```C++
# include <bits/stdc++.h>
# define ls p<<1
# define rs p<<1|1
using namespace std;
typedef long long ll;
const int N=10000003;
const int L=10000000;
const int R=10200000;
ll INF = 0x3f3f3f3f3f3f3f3f;
struct ST{
    ll sum, lmax, rmax, dat;
    int l, r;
}t[N << 2];
ll a[N];
void init(ST&t, int v) { t.dat=t.lmax=t.rmax=t.sum=v; }
void push_up(ST &p,ST &l,ST &r)
{
    p.sum=l.sum+r.sum;
    p.lmax=max(l.lmax,l.sum+r.lmax);
    p.rmax=max(r.rmax,r.sum+l.rmax);
    p.dat=max(l.rmax+r.lmax,max(l.dat,r.dat));
}
void build(int p, int l, int r){
    t[p].l = l, t[p].r = r;
    if (l == r){
        init(t[p],a[l]);
        return;
    }
    int mid = (l + r) >> 1;
    build(ls, l, mid); build(rs, mid + 1, r);
    push_up(t[p],t[ls],t[rs]);
}
void update(int p, int x, int v){
    if (t[p].l == t[p].r) {
        init(t[p], t[p].dat+v);
        return;
    }
    int mid = (t[p].l + t[p].r) >> 1;
    if (x <= mid) update(ls, x, v);
    else update(rs, x, v);
    push_up(t[p],t[ls],t[rs]);
}
ST que(int p, int l, int r)
{
    if (l <= t[p].l && r >= t[p].r) return t[p];
    int mid = (t[p].l + t[p].r) >> 1;
    if(r<=mid) return que(ls,l,r);
    if(l>mid) return que(rs,l,r);
    ST left=que(ls,l,r),right=que(rs,l,r),res;
    push_up(res,left,right);
    return res;
}
int t0,t1,t2;
int gen(){
    int x=t0,k=(t0+t1+t2)%N;
    t0=t1;t1=t2;t2=k;
    return x;
}
ll S(int N,int M){
    memset(t,0,sizeof(t));
    t0=t1=0;t2=1;
    ll ans=0;
    build(1,0,N-1);
    for(int i=1;i<=M;i++){
        int p=gen();
        int d=gen()*2-N+1;
        update(1,p,d);
        ans+=que(1,0,N-1).dat;
    }
    return ans;
}
int main(){
    printf("%lld\n",S(N,R)-S(N,L));
}

```

```C++
# include <bits/stdc++.h>
# define ls p<<1
# define rs p<<1|1
using namespace std;
typedef long long ll;
const int N=10000003;
const int L=10000000;
const int R=10200000;
ll INF = 0x3f3f3f3f3f3f3f3f;
struct ST{
    ll sum, lmax, rmax, dat;
    int l, r;
}t[N << 2];
ll a[N];
void init(ST&t, int v) { t.dat=t.lmax=t.rmax=t.sum=v; }
void push_up(ST &p,ST &l,ST &r)
{
    p.sum=l.sum+r.sum;
    p.lmax=max(l.lmax,l.sum+r.lmax);
    p.rmax=max(r.rmax,r.sum+l.rmax);
    p.dat=max(l.rmax+r.lmax,max(l.dat,r.dat));
}
void build(int p, int l, int r){
    t[p].l = l, t[p].r = r;
    if (l == r){
        init(t[p],a[l]);
        return;
    }
    int mid = (l + r) >> 1;
    build(ls, l, mid); build(rs, mid + 1, r);
    push_up(t[p],t[ls],t[rs]);
}
void update(int p, int x, int v){
    if (t[p].l == t[p].r) {
        init(t[p], t[p].dat+v);
        return;
    }
    int mid = (t[p].l + t[p].r) >> 1;
    if (x <= mid) update(ls, x, v);
    else update(rs, x, v);
    push_up(t[p],t[ls],t[rs]);
}
ST que(int p, int l, int r)
{
    if (l <= t[p].l && r >= t[p].r) return t[p];
    int mid = (t[p].l + t[p].r) >> 1;
    if(r<=mid) return que(ls,l,r);
    if(l>mid) return que(rs,l,r);
    ST left=que(ls,l,r),right=que(rs,l,r),res;
    push_up(res,left,right);
    return res;
}
int t0,t1,t2;
int gen(){
    int x=t0,k=(t0+t1+t2)%N;
    t0=t1;t1=t2;t2=k;
    return x;
}
ll T(int N,int L,int R){
    memset(t,0,sizeof(t));
    t0=t1=0;t2=1;
    ll ans=0;
    for(int i=1;i<=L;i++){
        int p=gen();
        int d=gen()*2-N+1;
        a[p]+=d;
    }
    build(1,0,N-1);
    for(int i=L+1;i<=R;i++){
        int p=gen();
        int d=gen()*2-N+1;
        update(1,p,d);
        ans+=que(1,0,N-1).dat;
    }
    return ans;
}
int main(){
    printf("%lld\n",T(N,L,R));
}

```
