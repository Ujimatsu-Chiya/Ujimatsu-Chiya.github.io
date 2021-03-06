---
title: Project Euler 342
tags:
  - Project Euler
mathjax: true
date: 2022-07-27 23:50:30
---

<escape><!-- more --></escape>

# Project Euler 342

## 题目

### The totient of a square is a cube

Consider the number $50$.

$50^2 = 2500 = 2^2 \times 5^4$, so $\varphi(2500) = 2 \times 4 \times 5^3 = 8 \times 5^3 = 2^3 \times 5^3. \ ^1$

So $2500$ is a square and  $\varphi(2500)$ is a cube.

Find the sum of all numbers $n$, $1 < n < 10^{10}$ such that $\varphi(n^2)$ is a cube.

$^1\ \varphi$ denotes **Euler's totient function**.

## 解决方案

根据欧拉函数的定义，不难知道$\varphi(n^2)=n\cdot\varphi(n)$。

由于$\varphi(p^e)=(p-1)p^{e-1}$，因子$(p-1)$将会包含更小的质因子。因此枚举$n$时，从大到小枚举质因子。

另外，$p^e\cdot \varphi(p^e)=(p-1)p^{2e-1}$。对于大的质因子而言，只有当$e\equiv2(\mod3)$时，枚举的$n$才有可能满足$n\cdot \varphi(n)$是一个平方数；但是欧拉函数值产生的因子$(p-1)$又会对以后枚举小的质因子造成影响，因此枚举时需要注意。

## 代码

```C++
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const ll N=10000000000;
const int M=sqrt(N);
bool vis[M+4];
int pr[M+4],m=0;
ll dfs(int p,ll n,ll phi){
    if(p==0) return n;
    ll t=phi;
    int c=0;
    for(;t%pr[p]==0;t/=pr[p],++c);
    ll ans=0;
    if(c%3==0) ans=dfs(p-1,n,phi);
    for(int e=1;;e++){
        n*=pr[p];
        if(n>=N) break;
        if((e+e-1+c)%3) continue;
        ans+=dfs(p-1,n,phi*(pr[p]-1));
    }
    return ans;
}
int main(){
    for(int i=2;i<=M;i++){
        if(!vis[i]){
            pr[++m]=i;
            for(int j=i+i;j<=M;j+=i)
                vis[j]=1;
        }
    }
    ll ans=dfs(m,1,1)-1;
    printf("%lld\n",ans);
}

```
