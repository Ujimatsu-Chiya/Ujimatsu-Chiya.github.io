---
title: Project Euler 343
tags:
  - Project Euler
mathjax: true
date: 2022-07-08 17:06:16
---

<escape><!-- more --></escape>

# Project Euler 343

## 题目

### Fractional Sequences

For any positive integer $k$, a finite sequence $a_i$ of fractions $\dfrac{x_i}{y_i}$ is defined by:

$a_1 = \dfrac{1}{k}$ and $a_i = \dfrac{x_{i-1}+1}{y_{i-1}-1}$ reduced to lowest terms for $i>1$.

When $a_i$ reaches some integer $n$, the sequence stops. (That is, when $y_i=1$.)

Define $f(k) = n$.

For example, for $k = 20$:

$\dfrac{1}{20} \rightarrow \dfrac{2}{19} \rightarrow \dfrac{3}{18} = \dfrac{1}{6} \rightarrow \dfrac{2}{5} \rightarrow \dfrac{3}{4} \rightarrow \dfrac{4}{3} \rightarrow \dfrac{5}{2} \rightarrow \dfrac{6}{1} = 6$

So $f(20) = 6$.

Also $f(1) = 1, f(2) = 2, f(3) = 1$ and $\sum f(k^3) = 118937$ for $1 \le k \le 100$.

Find $\sum f(k^3)$ for $1 \le k \le 2\times10^6$.

## 解决方案

在迭代求$a_i$的过程中，如果不发生约分，那么分子和分母之和总是相等的，这个和一开始为$k+1$。因此从一开始，在迭代的过程中，当分子$x_i$满足$\gcd(x_i,k+1)>1$时，那么就会进行约分。由于$x_i$是从$1$开始迭代的，因此发生约分的时候，$x_i$是$k+1$的最小质因数，设其为$p$。约分后，分子变成$1$，分母变成$(k+1-p)/p$，注意到也是一个新的分数单位，并且消去了$k+1$中最小的一个质因数$p$，此时是一个新的进入了新的迭代过程。

最终，$k+1$的质因子从小到大一直被消去，直到剩下一个最大的质因子。

如果一开始$k+1$是质数时，约分便不会再发生。故$f(k)$的值是$k+1$的最大质因子再减去$1$.

由于$n^3+1=(n+1)(n^2-n+1)$，$n^3+1$的最大质因子要么来自$n+1$，要么来自$n^2-n+1$。

求$n+1$的最大质因子此处不详述，使用普通筛法即可。而$n^2-n+1$则使用和216题类似的筛法进行筛选：令$g(n)=n^2-n+1$，如果$p|g(n)$，那么$p|g(kp+n),p|g(kp-n+1)$，其中$k>0$.

最终求$f(k^3)$时将两部分结果合并即可。

## 代码

```C++
# include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N=2e6;
ll v1[N+4],b[N+4],v2[N+4];
int main(){
    for(int i=2;i<=N+1;i++){
        if(v1[i]==0){
            for(int j=i;j<=N+1;j+=i)
                v1[j]=i;
        }
    }
    for(int i=1;i<=N;i++)
        v1[i]=v1[i+1];
    for(int i=1;i<=N;i++)
        b[i]=1ll*i*i-i+1;
    for(int i=2;i<=N;i++){
        ll p=b[i];
        if(p==1) continue;
        for(ll j=i;j<=N;j+=p)
            while(b[j]%p==0)
                b[j]/=p,v2[j]=max(v2[j],p);
        for(ll j=p-i+1;j<=N;j+=p)
            while(b[j]%p==0)
                b[j]/=p,v2[j]=max(v2[j],p);
    }
    ll ans=0;
    for(int i=1;i<=N;i++)
        ans+=max(v1[i],v2[i])-1;
    printf("%lld\n",ans);
}

```
