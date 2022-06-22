---
title: Project Euler 518
tags:
  - Project Euler
mathjax: true
date: 2022-06-22 23:27:09
---

<escape><!-- more --></escape>

# Project Euler 518

## 题目

### Prime triples and geometric sequences

Let $S(n) = a+b+c$ over all triples $(a,b,c)$ such that:

- $a, b$, and $c$ are prime numbers.
- $a < b < c < n$.
- $a+1, b+1$, and $c+1$ form a **geometric sequence**.

For example, $S(100) = 1035$ with the following triples:

$\begin{aligned}
& (2, 5, 11), (2, 11, 47), (5, 11, 23), (5, 17, 53), (7, 11, 17), (7, 23, 71), (11, 23, 47), \\
& (17, 23, 31), (17, 41, 97), (31, 47, 71), (71, 83, 97)
\end{aligned}$

Find $S(10^8)$.

## 解决方案

如果$a+1,b+1,c+1$是一个等比数列，那么不难观察出$(b+1)^2=(a+1)(c+1)$。

那么，不难发现，如果$a+1$有一些质因子$p$的指数是奇数，那么为了确保$b+1$是一个平方数，$c+1$的质因子$p$的指数也必须是奇数。

假设函数$f$定义如下：$f(n)=m$意味着$m$是最小的因子使得$\dfrac{n}{m}$是平方数。

如果两个质数$p,q$满足$f(p+1)=f(q+1)$，那么这对$(p,q)$才**有可能**产生一个答案。因此维护一些[链表](https://en.wikipedia.org/wiki/Linked_list#:~:text=Comparison%20of%20list%20data%20structures%20%20%20,%28%20n%20%29%20%203%20more%20rows%20)，这些链表用于存储$f$值相等情况下的$n$。

由于函数$f$值是无平方因子数，因此这些链表的数量比较多，长度也比较短，那么可以在每条链表上进行二重循环，枚举$a+1,c+1$的值。最终计算出$b=\sqrt{(a+1)(c+1)}-1$后，判断$b$是否为质数即可。

## 代码

```C++
#include <bits/stdc++.h>
#include "tools.h"
typedef long long ll;
using namespace std;
const int N=1e8;
const int M=N+1;
int v[M+4],pr[M/10+1000],f[M+4],head[M+4],pre[M+4];
int m=0;
int main(){
    for(int i=2;i<=N;i++){
        if(v[i]==0){
            f[i]=i;v[i]=i;pr[++m]=i;
        }
        for(int j=1;j<=m;j++){
            if(pr[j]>v[i]||pr[j]>N/i) break;
            v[i*pr[j]]=pr[j];
            f[i*pr[j]]=(f[i]%pr[j]==0?f[i]/pr[j]:f[i]*pr[j]);
        }
    }
    for(int i=1;i<=m&&pr[i]<=N;i++){
        int w=pr[i]+1;
        pre[w]=head[f[w]];
        head[f[w]]=w;
    }
    ll ans=0;
    for(int i=1;i<=N;i++)
        for(ll p=head[i];p;p=pre[p])
            for(ll q=pre[p];q;q=pre[q]){
                ll s= int_sqrt(1ll*p*q);
                if(v[s-1]==s-1) ans+=p+q+s-3;
            }
    printf("%lld\n",ans);

}
```
