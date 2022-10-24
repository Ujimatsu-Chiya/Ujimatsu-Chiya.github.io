---
title: Project Euler 27
category:
  - Project Euler
tags:
mathjax: true
date: 2022-04-27 09:56:23
---

<escape><!-- more --></escape>

# Project Euler 27

## 题目

### Quadratic primes

Euler discovered the remarkable quadratic formula:
$$n^2 + n + 41$$
It turns out that the formula will produce $40$ primes for the consecutive integer values $0 \le n \le 39$. However, when $n = 40$, $40^2 + 40 + 41 = 40(40 + 1) + 41$ is divisible by $41$, and certainly when $n = 41$, $41^2 + 41 + 41$ is clearly divisible by $41$.

The incredible formula $n^2 - 79n + 1601$ was discovered, which produces $80$ primes for the consecutive values $0 \le n \le 79$. The product of the coefficients, $−79$ and $1601$, is $−126479$.

Considering quadratics of the form: $n^2 + an + b$, where $|a|\lt 1000$ and $|b| \le 1000$;<br>where $|n|$ is the modulus/absolute value of $n$, e.g. $|11| = 11$ and $|-4| = 4$.

Find the product of the coefficients, $a$ and $b$, for the quadratic expression that produces the maximum number of primes for consecutive values of $n$, starting with $n = 0$.

## 解决方案

设$p(n)=n^2+an+b$

先用筛法将所有素数筛选出来（这里筛选的是范围$1000\times1000+40$以内的素数）。

然后通过枚举$a,b$的值，再用变量$n$判断长度。

一个优化：$b$必须是一个正数，并且是一个质数。因为当一开始$n=0$时，判断的值就是$f(0)=b$本身。

另一个优化：$a$可以从$1-b$开始枚举。因为$f(1)=a+b+1\ge2$ ，因此$a\ge 1-b$。

不过，加上了第二个优化后，需要额外进行一些细节上的判断，详见代码。

## 代码

```C++
# include <bits/stdc++.h>
typedef long long ll;
using namespace std;
const int M=2;
const int N=M*M+40;
bool v[N+4];
vector<int>pr;
int main(){
    for(int i=2;i<=N;i++){
        if(v[i]) continue;
        if(i<=M) pr.push_back(i);
        for(ll j=1ll*i*i;j<=N;j+=i)
            v[j]=1;
    }
    v[0]=v[1]=1;
    int ans=0,mx=0,n;
    for(int b:pr)
        for(int a=1-b;a<=M-1;++a){
            for(n=0;n*n+n*a+b>=0&&!v[n*n+n*a+b];++n);
            if(n>mx) mx=n,ans=a*b;
        }
    printf("%d\n",ans);
}
```
