---
title: Project Euler 621
category:
  - Project Euler
tags:
  - 论文
mathjax: true
date: 2022-08-05 21:41:55
---

<escape><!-- more --></escape>

# Project Euler 621

## 题目

### Expressing an integer as the sum of triangular numbers

Gauss famously proved that every positive integer can be expressed as the sum of three **triangular numbers** (including $0$ as the lowest triangular number). In fact most numbers can be expressed as a sum of three triangular numbers in several ways.

Let $G(n)$ be the number of ways of expressing $n$ as the sum of three triangular numbers, regarding different arrangements of the terms of the sum as distinct.

For example, $G(9)=7$, as 9 can be expressed as: $3+3+3, 0+3+6, 0+6+3, 3+0+6, 3+6+0, 6+0+3, 6+3+0$.

You are given $G(1000)=78$ and $G(10^6)=2106$.

Find $G(17526\times10^9)$.

## 解决方案

令$n=\dfrac{a(a+1)}{2}+\dfrac{b(b+1)}{2}+\dfrac{c(c+1)}{2}$.

那么可以变形得：

$$8n+3=(2a+1)^2+(2b+1)^2+(2c+1)^2$$

令$r_3(n)$表示将一个数$n$写成$3$个奇数的平方的方法数，那么得$G(n)=r_3(8n+3)$。不难发现只有当$n$满足$n\equiv 3 \pmod 8$时，$r_3(n)>0$才成立。

这篇[论文](http://www.personal.psu.edu/jxs23/p7.pdf)给出了一个关于$r_3$的递推式：

$$r_3(9^\lambda n) =
\begin{cases}
3^\lambda \times r_3(n), & \text{if }n \equiv 11 \pmod{24} \\
(2\times3^\lambda -1) \times r_3(n) & \text{if } n \equiv 19 \pmod{24} \\
\dfrac{3^{\lambda+1}-1}{2} \times r_3(n) & \text{if } n \equiv 3 \text{ or } 51 \pmod{72}
\end{cases}$$

由于$17526\times 10^9\times 8+3=3^8 \times 13 \times 3527 \times 466073$。因此计算时我们仅需考虑去掉$9^{\lambda}$后的$n$。令$M=13 \times 3527 \times 466073$，也就是$r_3(M)$。

到了这一步，从小到大枚举奇数$i$，求解$r_2'(M-i^2)$，其中$r_2'(m)$表示方程$x^2+y^2=m$有多少对$(x,y)$都是**奇数**，也是**正整数**的解。

[页面1](https://en.wikipedia.org/wiki/Sum_of_squares_function#Formulae#)，[页面2](https://mathworld.wolfram.com/SumofSquaresFunction.html)给出了一个信息：如果$n$可以将其分解成$n=2^g\prod_i p_i^{e_i}\prod_j q_j^{f_j}$，其中$p_i$是模$4$余$1$的质数，$q_j$是模$4$余$3$的质数。那么方程$x^2+y^2=m$的解的个数由$r_2(m)$决定：

$$r_2(n)=
\left \{\begin{aligned}
  &0  & & \text{if}\quad  \exists j,f_j\equiv 1\pmod 2 \\
  &4\prod_i(e_i+1) & & \text{else}
\end{aligned}\right.
$$

由于目前只求正整数解，那么在求出$r_2$的基础上需要再除$4$。

那么现在引入了一个麻烦：$r_2$是求所有解的个数，但是我们现在需要求的是$x,y$奇数解，怎么去掉潜在的偶数解？

实际上对于任意一个$t$，如果$2\mid t,4\nmid t$，那么方程$x^2+y^2=t$明显不存在$x,y$同为偶数的解。而上面这种数$t=8n+3-i^2$实际上是满足这种情况的。令$i=2k+1,k\ge 0$，那么就可以写成：

$$t=8n+3-i^2=8n+3-(2k+1)^2=8n-4k^2-4k+2\equiv2\pmod 4$$

因此，$r_2'(M-i^2)=\dfrac{r_2(M-i^2)}{4}$。直接枚举奇数$i$，对$r_2'(M-i^2)$求和即可。回代到上面的递推公式求出最终值。

## 代码

```C++
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const ll Q = 17526000000000;
const int N = 10000000;

int v[N + 1];
int pr[N/5+1000],m=0;

ll r2(ll n) {
    ll ans=1;
    if (n<=N) {
        for(;n!=1;){
            int p=v[n],c=0;
            for(;n%p==0;n/=p,++c);
            if(p%4==3){
                if(c&1) return 0;
            }
            else if(p%4==1) ans*=(c+1);
        }
    } else {
        for(int i=1;i<=m&&1ll*pr[i]*pr[i]<=n&&n>N;i++){
            int p=pr[i],c=0;
            for(;n%p==0;n/=p,++c);
            if(p%4==3){
                if(c&1) return 0;
            }
            else if(p%4==1) ans*=(c+1);
        }
        if(n<N) return ans*r2(n);
        else if(n>1){
            if(n%4==3) return 0;
            else if(n%4==1) ans*=2;
        }
    }
    return ans*4;
}
ll r3(ll n) {
    ll ans=0;
    for (ll i=1;i*i<=n;i+=2)
        ans+=r2(n-i*i);
    ans*=2;
    return ans;
}

ll G(ll n) {
    ll m=n*8+3,pw3=1;
    for(;m%9==0;m/=9,pw3*=3);
    ll ans;
    if(m%24==11) ans=pw3*r3(m);
    else if(m%24==19) ans=(pw3*2-1)*r3(m);
    else if(m%72==27) ans=r3(m*pw3*pw3);
    else ans=(pw3*3-1)/2*r3(m);
    return ans/8;
}

int main() {
    v[1]=1;
    for(int i=2;i<=N;i++){
        if(v[i]==0){
            pr[++m]=i;
            v[i]=i;
        }
        for(int j=1;j<=m;j++){
            if(pr[j]>v[i]||pr[j]>N/i) break;
            v[i*pr[j]]=pr[j];
        }
    }
    ll ans = G(Q);
    printf("%lld\n",ans);
}

```
