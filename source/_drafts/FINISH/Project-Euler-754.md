---
title: Project Euler 754
tags:
  - Project Euler
  - 容斥原理
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 754
## 题目
### Product of Gauss Factorials


The **Gauss Factorial** of a number $n$ is defined as the product of all positive numbers $\leq n$ that are relatively prime to $n$. For example $g(10)=1\times 3\times 7\times 9 = 189$. 
Also we define
$$\displaystyle G(n) = \prod_{i=1}^{n}g(i)$$
You are given $G(10) = 23044331520000$.

Find $G(10^8)$. Give your answer modulo $1\,000\,000\,007$.


## 解决方案

令函数$f(N,n)$表示在$n< i\le N$这些数中，有多少个$i$满足$\gcd(n,i)=1.$那么$G(N)$就可以写成：

$$G(N)=\prod_{n=2}^N n^{f(N,n)}$$

其中，通过容斥原理和莫比乌斯函数$\mu$的性质，不难写出

$$f(N,n)=\sum_{d|n}\mu(d)(\lfloor\dfrac{N}{d}\rfloor-\lfloor\dfrac{n}{d}\rfloor)$$

注意式子后面第二项是减去$n$以内的数。

最终直接进行计算即可，时间复杂度为$O(N\log N)$。


## 代码

本代码运行超过$1$分钟（约$70$秒），我暂时没有比较好的思路来优化这道题。

```C++
# include <bits/stdc++.h>
using namespace std;
const int N=1e8;
int mod=1000000007;
int qpow(int n,int m){
    int ans=1;
    for(;m;m>>=1){
        if(m&1) ans=1ll*ans*n%mod;
        n=1ll*n*n%mod;
    }
    return ans;
}
char mu[N+1];
bool vis[N+1];
int f[N+1];
int pr[N/10+100],m=0;
int main(){
    mu[1]=1;
    for(int i=2;i<=N;i++){
        if(!vis[i]){
            pr[++m]=i;
            vis[i]=1;mu[i]=-1;
        }
        for(int j=1;j<=m;j++){
            if(pr[j]>N/i) break;
            vis[i*pr[j]]=1;
            if(i%pr[j]) mu[i*pr[j]]=-mu[i];
            else{
                mu[i*pr[j]]=0;break;
            }
        }
    }
    for(int d=1;d<N;d++){
        if(mu[d]==0) continue;
        for(int n=d;n<=N;n+=d)
            f[n]+=mu[d]*(N/d-n/d);
    }
    int ans=1;
    for(int n=2;n<=N;n++)
        ans=1ll*ans*qpow(n,f[n])%mod;
    printf("%d\n",ans);
}

```