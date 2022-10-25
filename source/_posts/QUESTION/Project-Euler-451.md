---
title: Project Euler 451
category:
  - Project Euler
tags:
mathjax: true
date: 2022-07-12 00:16:47
---

<escape><!-- more --></escape>

# Project Euler 451

## 题目

### Modular inverses

Consider the number $15$.

There are eight positive numbers less than $15$ which are coprime to $15: 1,2, 4, 7, 8, 11, 13, 14$.

The modular inverses of these numbers modulo 15 are: $1, 8, 4, 13, 2, 11, 7, 14$ because

$\begin{aligned}
1 \cdot 1 &\bmod 15=1\\
2 \cdot 8=16 &\bmod 15=1\\
4 \cdot 4=16 &\bmod 15=1\\
7 \cdot 13=91 &\bmod 15=1\\
11 \cdot 11=121 &\bmod 15=1\\
14 \cdot 14=196 &\bmod 15=1
\end{aligned}$

Let $I(n)$ be the largest positive number $m$ smaller than $n-1$ such that the modular inverse of $m$ modulo $n$ equals $m$ itself.

So $I(15)=11$.

Also $I(100)=51$ and $I(7)=1$.

Find $\sum I(n)$ for $3\le n\le2\cdot10^7$

## 解决方案

将问题进行正式描述：求$I(n)$的值，其中$I(n)$是方程$x^2\equiv 1\pmod n$中，小于$n-1$的最大正整数解。方程也可以化为：

$$(x+1)(x-1)\equiv 0\pmod n\qquad(1)$$

假设$n$的分解质因数为$n=\prod_{i=1}^{k} p_i^{e_i}$，那么不难发现：

1. 对于任意一个$p_i$为**奇数**的$p_i^{e_i}$，要么$p_i^{e_i}\mid x-1$，要么$p_i^{e_i}\mid (x+1)$，因此方程$(x+1)(x-1)\equiv 0 \pmod {p_i^{e_i}}$只有两个解：$1,-1$。
2. 对于$2^{e}$，在保持上面的性质的基础上，可以发现$4$并不能整除$(x+1)$和$(x-1)$，但是$2$可以，因此对于方程$(x+1)(x-1)\equiv 0\pmod {2^e}$一共有$4$个解：$1,-1,2^{e-1}-1,2^{e-1}+1$.当$e\le 2$时，需要将这些值相同的解合并。

最终，对于每个$p_i^{e_i}$分量，方程$(x+1)(x-1)\equiv 0 \pmod {p_i^{e_i}}$都有多个解。通过中国剩余定理将它们进行合并成原方程$(1)$的解再取最大值即可。

不过由于数据范围$N=2\times 10^7$，比较大，因此实际上实现的时候，使用中国剩余定理先将多个形如$x^2\equiv 1\pmod {p_i^{e_i}}$方程的解两个两个地进行组合。具体方式如下：

假设$n'=\prod_{i=1}^{k'}p_i^{e_i},k'< k,m=p_{k'+1}^{e_{k'+1}}$，如果我们已经解出了$x^2\equiv 1 \pmod {n'}$的所有解，那么再方程的所有解$x_b$和方程$x^2\equiv 1 \pmod {m}$的所有解$x_a$（注意$x_a$要么为$1$，要么为$-1$）一一组合，得到如下方程组：

$$
\left \{\begin{aligned}
  & x\equiv x_a\pmod {m}\\
  & x\equiv x_b\pmod {n'}\\
\end{aligned}\right.
$$

令$x=t_am+x_a=t_bn'+x_b$，那么得到一个以$t_a$和$t_b$为未知数的方程$t_am-t_bn'=x_b-x_a$.

通过扩展欧几里得算法，我们可以解得方程$t_a'm-t_b'n'=1$的解$(t_a',t_b')$。那么得到$t_a=(x_b-x_a)t_a'$

那么得到$x=t_am+x_a=(x_b-x_a)t_a'm+x_a=x_bt_a'm+x_a(1-t'_am)$。由于$x_a$能够分别取$1$和$-1$，因此每合并一个方程，都能够产生两个解：$x_bt_a'm\pm(1-t'_am)$

## 代码

```C++
#include <bits/stdc++.h>
# define lb(x) ((x)&(-x))
using namespace std;
typedef long long ll;
const int N=2e7;
int qpow(ll n,ll m,ll mod){
    ll a=1;
    for(;m;m>>=1){
        if(m&1) a=a*n%mod;
        n=n*n%mod;
    }
    return a;
}
int mxp[N+4];
int a[1004],c=0;
int r[14],m=0;
int main(){
    for(int p=3;p<=N;p++)
        if(!mxp[p])
            for(int i=p;i<=N;i+=p) mxp[i]=p;
    ll ans=0;
    for(int i=3;i<=N;i++){
        m=c=0;
        int pw2=lb(i);
        if((pw2&1)==0){
            a[c++]=1;
            if((pw2&2)==0){
                a[c++]=pw2-1;
                if((pw2&4)==0){
                    a[c++]=(pw2>>1)+1;
                    a[c++]=(pw2>>1)-1;
                }
            }
        }
        else a[c++]=0;
        int mul=pw2;
        for(int v=i/mul;v!=1;){
            int p=mxp[v],pw=1;
            for(;v%p==0;v/=p,pw*=p);
            int nmul=mul*pw;
            ll x=qpow(mul,pw/p*(p-1)-1,pw)*mul%nmul;
            ll y=1ll-x;
            for(int pc=c,j=0;j<pc;j++){
                a[c++]=(a[j]*y+x)%nmul;
                a[j]=(a[j]*y-x)%nmul;
            }
            mul=nmul;
        }
        int mx=0;
        for(int j=0;j<c;j++){
            if(a[j]<0) a[j]+=i;
            if(a[j]!=i-1) mx=max(mx,a[j]);
        }
        ans+=mx;
    }
    printf("%lld\n",ans);
}

```
