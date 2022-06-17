---
title: Project Euler 221
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    

# Project Euler 221
## 题目
### Alexandrian Integers

We shall call a positive integer $A$ an “Alexandrian integer”, if there exist integers $p, q, r$ such that:

$$A=p·q·r \text{ and } \frac{1}{A}=\frac{1}{p}+\frac{1}{q}+\frac{1}{r}$$

For example, $630$ is an Alexandrian integer ($p = 5, q = -7, r = -18$). 

In fact, $630$ is the $6^{\text{th}}$ Alexandrian integer,  the first $6$ Alexandrian integers being: $6, 42, 120, 156, 420$ and $630$.

Find the $150000^{\text{th}}$ Alexandrian integer.


## 解决方案

可以发现，$p,q,r$中必定有其中一个数是正数，其余两个数是负数，假设$p$是正数，$q,r$是负数。

因此问题等价于如下形式：

寻找$A=pqr$，其中$p,q,r>0$，使得$\dfrac{1}{A}=\dfrac{1}{p}-\dfrac{1}{q}-\dfrac{1}{r}$

消去$A$，不难得到

$$qr-pr-qp=1$$

两边都加一个$p^2$，那么可以写成

$$(p-q)(p-r)=p^2+1$$

那么，先枚举$p$，再枚举$p^2+1$的因子$d$，那么可以得到$p-q=d,p-r=\dfrac{p^2+1}{d}$，最终得到题目中要求的一个数：

$$A=p(p+d)(p+\dfrac{p^2+1}{d})$$

令$f(n)=n^2+1$，那么使用216题的分解方式对$f(n)$进行分解：如果$p|f(n)$，那么$p|f(kp\pm n)$，其中$k>0$。再根据分解产生其所有因子。

本题$p$的上限难以确定，如果查询的值为$Q=150000$，那么就假设为$\dfrac{2Q}{3}+100$。

## 代码

```C++
#include <bits/stdc++.h>
typedef long long ll;
using namespace std;
const int Q = 150000;
const int M = Q*2/3+100;
const ll MX = 1e18;
ll f[M+4];
unordered_map<ll,int>fact[M+4];
int main(){
    for(int i=1;i<=M;i++)
        f[i]=1ll*i*i+1;
    for(int i=1;i<=M;i++){
        ll p=f[i];
        if(p==1) continue;
        for(ll j=i;j<=M;j+=p)
            while(f[j]%p==0) f[j]/=p,++fact[j][p];
        for(ll j=p-i;j<=M;j+=p)
            while(f[j]%p==0) f[j]/=p,++fact[j][p];
    }
    vector<ll>a;
    for(ll p=1; p <= M; p++){
        ll n= p*p+1;
        vector<ll>divs{1};
        for(auto &[pr,e]:fact[p]){
            int l=0,r=divs.size();
            for(int _ = 0;_ < e;_++){
                for(int j=l;j<r;j++)
                    if(divs[j]*divs[j]*pr*pr<=n)
                        divs.push_back(divs[j]*pr);
                l=r;r=divs.size();
            }
        }
        for(ll d:divs){
            if(p*(p+d)>MX/(p+(p*p+1)/d)) continue;
            a.push_back(p*(p+d)*(p+(p*p+1)/d));
        }
    }
    sort(a.begin(),a.end());
    ll ans=a[Q-1];
    printf("%lld\n",ans);
}
```
