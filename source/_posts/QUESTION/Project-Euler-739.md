---
title: Project Euler 739
tags:
  - Project Euler
mathjax: true
date: 2022-07-17 23:12:00
---

<escape><!-- more --></escape>

# Project Euler 739

## 题目

### Summation of Summations

Take a sequence of length $n$. Discard the first term then make a sequence of the partial summations. Continue to do this over and over until we are left with a single term. We define this to be $f(n)$.

Consider the example where we start with a sequence of length $8$:

$
\begin{array}{rrrrrrrr}
1&1&1&1&1&1&1&1\\
 &1&2&3&4&5& 6 &7\\
 & &2&5&9&14&20&27\\
 & & &5&14&28&48&75\\
 & & & &14&42&90&165\\
 & & & & & 42 & 132 & 297\\
 & & & & & & 132 &429\\
 & & & & & & &429\\
\end{array}
$

Then the final number is $429$, so $f(8) = 429$.

For this problem we start with the sequence $1,3,4,7,11,18,29,47,\ldots$

This is the Lucas sequence where two terms are added to get the next term.

Applying the same process as above we get $f(8) = 2663$.

You are also given $f(20) = 742296999 $ modulo $1\,000\,000\,007$

Find $f(10^8)$. Give your answer modulo $1\,000\,000\,007$.

## 解决方案

不难想到，如果第一行是序列$[a_0,a_1,a_2,\dots,a_{n-1}]$，那么经过变换后，最后得出来的数必定是$a$中这些数的线性组合$\sum_{k=0}^{n-1}C(n,k)\cdot a_k$，其中$C(n,k)$是系数。

那么我们就转为求出序列$[C(n,0),C(n,1),C(n,2),\dots,C(n,n-1)]$.

为了暴力求出$C(n,k)$，那么就将初始化一个长度为$n$的全$0$序列，然后令第$k$个值为$1$。经过上面的迭代后，将求出的值查询OEIS，结果为[A106566](https://oeis.org/A106566).找到FORMULA一栏的信息：

``` 
T(n, k) = binomial(2n-k-1, n-k)*k/n for 0 <= k <= n with n > 0; T(0, 0) = 1; T(0, k) = 0 if k > 0.
```

这直接给出了关于$C$的公式：

$$C(n+1,i)=\dfrac{k\cdot C_{2n-k-1}^{n-k}}{n}$$
由此直接计算即可。


额外的发现。对于$n>1$的情况下，$C(n,k)$的所有值是上面这个三角形的第$n-1$列的逆序，并且$0$还被排除了，这里参考[A009766](http://oeis.org/A009766)。

## 代码

```C++
#include <bits/stdc++.h>
typedef long long ll;
using namespace std;
const int N = 1e8;
const int M = N*2;
const int n=N-1;
ll mod=1e9+7;
ll inv(ll n,ll p){
    ll ans=1,m=p-2;
    for(;m;m>>=1){
        if(m&1) ans=ans*n%mod;
        n=n*n%mod;
    }
    return ans;
}

int *fac,*finv;
int l[N+4],invn=inv(n,mod);
int C(int n,int m){
    return 1ll*fac[n]*finv[m]%mod*finv[n-m]%mod;
}
int T(int n,int k){
    if(n==0) return 0;
    else return 1ll*C(2*n-k-1,n-k)*k%mod*invn%mod;
}
int main(){
    fac = new int[M+4];
    finv = new int[M+4];
    fac[0]=fac[1]=1;
    finv[0]=1;
    for(int i=2;i<=M;i++)
        fac[i]=1ll*fac[i-1]*i%mod;
    finv[M]=inv(fac[M],mod);
    for(int i=M-1;i>0;i--)
        finv[i]=1ll*finv[i+1]*(i+1)%mod;
    int x=1,y=3;
    int ans=0;
    for(int i=0;i<=n;i++){
        ans=(ans+1ll*T(n,i)*x)%mod;
        int t=(x+y)%mod;
        x=y;y=t;
    }
    delete fac;
    delete finv;
    printf("%d\n",ans);
}
```