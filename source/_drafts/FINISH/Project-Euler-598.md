---
title: Project Euler 598
category:
  - Project Euler
tags:
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 598
## 题目
### Split Divisibilities



Consider the number $48$.

There are five pairs of integers $a$ and $b$ ($a \leq b$) such that $a \times b=48: (1,48), (2,24), (3,16), (4,12)$ and $(6,8)$.

It can be seen that both $6$ and $8$ have $4$ divisors.

So of those five pairs one consists of two integers with the same number of divisors.

In general: Let $C(n)$ be the number of pairs of positive integers $a \times b=n$, ($a \leq b$) such that $a$ and $b$ have the same number of divisors; so $C(48)=1$.

You are given $C(10!)=3: (1680, 2160), (1800, 2016)$ and $(1890,1920)$. 

Find $C(100!)$




## 解决方案


令$n$的分解为$n=\prod_{i=1}^k p_i^{e_i}$，那么我们得到一个$k$维向量$\vec{e}=[e_1,e_2,\dots,e_k]$。根据因数个数定理$\sigma_0(n)=\prod_{i=1}^k(e_i+1)$，那么问题转化为如下形式：

求有多少个$k$维向量$\vec{a}$，满足以下条件：

1. $\forall i \in [1,k],0\le b_i\le e_i$
2. $\prod_{i=1}^k (b_i+1)=\prod_{i=1}^k(e_i-b_i+1)$，也就是$\prod_{i=1}^k\dfrac{b_i+1}{e_i-b_i+1}=1$

可以发现，这些向量$b_i$和$n$的因子一一对应，因此最终答案就是这些向量个数的一半（注意还要考虑当$n$为平方数的情况）。

那么不难想到一种朴素的做法：如果目前已经针对前$j$个质因子的指数暴力枚举，并且用字典存储统计得到的$v=\prod_{i=1}^j\dfrac{b_i+1}{e_i-b_i+1}$的方案个数。那么暴力枚举$b_{j+1}$和字典中的每个$v$，用新字典存储$v\cdot \dfrac{b_{j+1}+1}{e_{j+1}-b_{j+1}+1}$的个数。

不过，这样直接暴力处理，之后字典产生的条目将会非常多，严重降低了效率。

假设向量$\vec{e}$已经降序排序，也就是$e_1\ge e_2\ge\dots\ge e_k$。由于我们最终需要求的$v$值是$1$，在计算完前$j$个项后，字典存储的$v$键都是以一个分数来表示。如果当前$v$的分子或者分母的**最大质因数**大于$e_{j+1}+1$，那么说明在后续操作中，这个最大质因子肯定不能被约掉，不能为最终$v=1$的情况做贡献，需要及时去除。

经过如此操作后，字典的值将会省略掉一大部分，提高了效率。

## 代码


```C++
# include <bits/stdc++.h>
# define X first
# define Y second
# define lb(x) ((x) & (-x))
# define mem(a,b) memset(a,b,sizeof(a))
# define debug freopen("r.txt","r",stdin)
# define pi pair<int,int>
using namespace std;
typedef long long ll;
typedef unsigned long long ull;

const int N=100;

struct Fraction{
    ll num,den;
    Fraction(ll n=1,ll d=0){
        ll g=__gcd(n,d);
        num=n/g;den=d/g;
    }
    Fraction operator + (Fraction f){
        return Fraction(num*f.den+den*f.num,den*f.den);
    }
    Fraction operator * (Fraction f){
        return Fraction(num*f.num,den*f.den);
    }
    Fraction inv(){
        return {den,num};
    }
    //这里的小于只是为了用于区分分数的不同，而并非是分数的值大小本身。
    bool operator < (const Fraction &f) const{
        return num<f.num||num==f.num&&den<f.den;
    }
};

bool vis[N+4];
int pr[N+4],m=0;
int e[N+4];
int cal(int n,int p){
    int ans=0;
    for(;n;n/=p) ans+=n/p;
    return ans;
}
int max_prime(ll n){
    if(n==1) return -1;
    int i;
    for(i=1;i<=m&&n!=1;){
        if(n%pr[i]==0) n/=pr[i];
        else ++i;
    }
    return pr[i];
}
map<Fraction,ll>mp[N+4];
int main(){
    //freopen("w.txt","w",stdout);
    for(int i=2;i<=N;i++){
        if(vis[i]) continue;
        pr[++m]=i;
        for(int j=i+i;j<=N;j+=i)
            vis[j]=1;
    }
    for(int i=1;i<=m;i++)
        e[i]=cal(N,pr[i]);
    for(int j=0;j<=e[1];j++)
        ++mp[1][Fraction(j+1,e[1]-j+1)];
    for(int i=2;i<m;i++){
        for(int j=0;j<=e[i];j++){
            Fraction t(j+1,e[i]-j+1);
            for(auto &[k,v]:mp[i-1]){
                Fraction f=t*k;
                if(max_prime(f.num)<=e[i+1]+1&&max_prime(f.den)<=e[i+1]+1){
                    mp[i][f]+=v;
                }
            }
        }
    }
    ll ans=0;
    for(int j=0;j<=e[m];j++){
        ans+=mp[m-1][Fraction(j+1,e[m]-j+1)];
    }
    ans>>=1;
    printf("%lld\n",ans);
}

```