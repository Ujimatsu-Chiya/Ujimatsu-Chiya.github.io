---
title: Project Euler 300
tags:
  - Project Euler
mathjax: true
date: 2022-07-06 13:08:20
---

<escape><!-- more --></escape>

# Project Euler 300

## 题目

### Protein folding

In a very simplified form, we can consider proteins as strings consisting of hydrophobic (H) and polar (P) elements, e.g. HHPPHHHPHHPH.

For this problem, the orientation of a protein is important; e.g. HPP is considered distinct from PPH. Thus, there are $2^n$ distinct proteins consisting of $n$ elements.

When one encounters these strings in nature, they are always folded in such a way that the number of H-H contact points is as large as possible, since this is energetically advantageous.

As a result, the H-elements tend to accumulate in the inner part, with the P-elements on the outside.

Natural proteins are folded in three dimensions of course, but we will only consider protein folding in <u>two dimensions</u>.

The figure below shows two possible ways that our example protein could be folded (H-H contact points are shown with red dots).

![](../images/p300_protein.gif)

The folding on the left has only six H-H contact points, thus it would never occur naturally.

On the other hand, the folding on the right has nine H-H contact points, which is optimal for this string.

Assuming that H and P elements are equally likely to occur in any position along the string, the average number of H-H contact points in an optimal folding of a random protein string of length $8$ turns out to be $\dfrac{850}{2^8}=3.3203125$.

What is the average number of H-H contact points in an optimal folding of a random protein string of length $15$?

Give your answer using as many decimal places as necessary for an exact result.

## 解决方案

一个很明显的事实：如果蛋白质序列的第$i$个和第$j$个元素在平面上相邻，那么$i$和$j$的奇偶性不相同。因此，我们假设偶数序号$e$和奇数序号$o$接触时，用一个编码来表示。这种编码方式的编码量是盲目编码时的约$\dfrac{1}{4}$。当$N=15$时，元素之间的接触情况可以用一个$64$位整数表示。

我的做法相对比较朴素。首先通过深度优先搜索枚举出所有可能出现的折叠情况，接下来枚举所有不同蛋白质的序列，和每种折叠情况一一组合比较，取最优的作为结果。

为了加速运行，我使用了以下策略：

1. 枚举折叠情况时，固定第$1$个蛋白质在第$0$个右面。因为蛋白质的折叠形状和本身的位置没有关系。

2. 去掉一些不可能最优的折叠情况。部分折叠情况的接触面集合是另外一个折叠情况的子集，这些折叠情况不可能对应到最优的折叠情况。

3. 使用蝴蝶变换求出每一个$N$比特数的逆序，并且某个顺序和其逆序的最大接触面数明显是一样的，只枚举其中一个。这可以减少一半的枚举量。

## 代码

```C++
# include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N=15;
int b[N+N+4][N+N+4];
int dx[4]={-1,1,0,0},dy[4]={0,0,-1,1};
int g[N][N];
set<ll>st;
void dfs(int fl,int px,int py,ll s){
    for(int i=0;i<4;i++){
        int nx=px+dx[i],ny=py+dy[i];
        if(b[nx][ny] != -1)
            s|=1ll << g[fl-1][b[nx][ny]];
    }
    if(fl==N){
        st.insert(s);
        return;
    }
    for(int i=0;i<4;i++){
        int nx=px+dx[i],ny=py+dy[i];
        if(b[nx][ny] == -1){
            b[nx][ny]=fl;
            dfs(fl+1,nx,ny,s);
            b[nx][ny]=-1;
        }
    }
}
//计算出对应的分子。
int rev[1<<N],mx[1<<N];
int solve(){
    memset(b, -1, sizeof(b));
    if(N==1) return 1;
    int m=0;
    for(int i=0;i<N;i+=2)
        for(int j=1;j<N;j+=2){
            g[i][j]= g[j][i]=m++;
        }
    b[N][N]=0;b[N][N+1]=1;
    dfs(2, N,N+1, g[0][1]);
    set<ll>t(st);st.clear();
    //去掉子集
    for(auto it=t.rbegin();it!=t.rend();it++){
        bool ok=1;
        for(ll x:st)
            if((x|*it)==x){
                ok=0;break;
            }
        if(ok) st.insert(*it);
    }
    int sum=0;
    for(int s=0;s<(1<<N);s++){
        //蝴蝶变换
        rev[s] = ((rev[s >> 1] >> 1)) | ((s & 1) << (N - 1));
        if(rev[s]<s) sum+=mx[rev[s]];
        else{
            ll y=0;
            for(int i=0;i<N;i+=2)
                for(int j=1;j<N;j+=2)
                    if((s>>i&1)&&(s>>j&1))
                        y|=1ll<<g[i][j];
            for(ll x:st)
                mx[s]=max(mx[s],__builtin_popcountll(x&y));
            sum+=mx[s];
        }
    }
    return sum;
}
int main(){
    int num=solve(),den=1<<N;
    int g=__gcd(num, den);
    num/=g;den/=g;
    int lg=log2(den + 1e-6);
    double ans=1.0*num/den;
    printf("%.*f\n", lg, ans);
}

```
