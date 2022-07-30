---
title: Project Euler 440
tags:
  - Project Euler
  - 矩阵快速幂
mathjax: true
date: 2022-07-27 23:50:13
---

<escape><!-- more --></escape>

# Project Euler 440

## 题目

### GCD and Tiling

We want to tile a board of length $n$ and height $1$ completely, with either $1 \times 2$ blocks or $1 \times 1$ blocks with a single decimal digit on top:

![](../images/p440_tiles.png)

For example, here are some of the ways to tile a board of length $n = 8$:

![](../images/p440_some8.png)

Let $T(n)$ be the number of ways to tile a board of length $n$ as described above.
For example, $T(1) = 10$ and $T(2) = 101$.

Let $S(L)$ be the triple sum $\sum_{a,b,c} \gcd(T(c^a), T(c^b))$ for $1 \le a, b, c \le L$.

For example:

$\begin{aligned}
&S(2) = 10444\\
&S(3) = 1292115238446807016106539989\\
&S(4) \mod 987 898 789 = 670616280.
\end{aligned}$

Find $S(2000) \mod 987 898 789$.

## 解决方案

令$N=2000$

不难知道递推式$T$满足$T(n)=10T(n-1)+T(n-2).$

根据此[页面](https://www.cnblogs.com/tkandi/p/10414428.html)关于线性递推式的性质，考虑将递推式在前面拼接两项$0,1$，成为$U$。那么可以写成$U(0)=0,U(1)=1,U(n)=10U(n-1)+U(n-2)$。

使用这个性质后，那么有$\gcd(U(n),U(m))=U(\gcd(n,m))$。

因此，问题转化为求$\sum_{a=1}^N\sum_{b=1}^N\sum_{c=1}^N U(\gcd(c^a+1,c^b+1)).$

为求解$\gcd(c^a+1,c^b+1)$，有以下结论：

- 若$g=\gcd(a,b)$，并且$\dfrac{a}{g},\dfrac{b}{g}$都是奇数，那么答案为$c^g+1$。
- 否则，当$c$为奇数时答案为$2$，当$c$为偶数时，答案为$1$。

根据欧几里得算法，$\gcd(c^a+1,c^b+1),a>b$可以进行如下变化：

$\begin{aligned}
&\gcd(c^a+1,c^b+1)=\gcd(c^a-c^b,c^b+1)=\gcd(c^{a-b}-1,c^b+1)=\gcd(c^{a-b}+c^b,c^b+1)\\
=&\gcd(c^{|a-2b|}+1,c^b+1)
\end{aligned}$

注意到迭代过程中，无论是$|a-2b|$还是$b$，都是$a,b$的线性组合。最后一轮迭代结束时，要么$a=b=g=\gcd(a,b)$，$\gcd(c^a+1,c^b+1)=c^g+1$；要么$b=0,c^b+1=2$（注意在此处，上一轮迭代情况将会有一个偶数$2g,|2b-2\cdot b|=0$）。

那么抛开$a,b$中的最大公因数$g$，单独讨论$a'=\dfrac{a}{g}$和$b'=\dfrac{b}{g}$。如果$a',b'$都是奇数，那么在迭代$(a',b')\rightarrow(|a'-2b'|,b')$的过程中，都不会出现$a',b'$中有一个是偶数的情况；如果其中一个是偶数，那么最终迭代的结果必将存在一个$a',b'$为$0$。

回到本问题，计算$S(N)$是一个三重循环，但是计算$\gcd(c^a+1,c^b+1)$时，迭代的阶段可以不需要知道$c$，只有最后的时候才需要代入$c$计算出具体值。因此我们先枚举$a,b$，保留中间值$?^{\gcd(a,b)}+1,3-?\mod 2$。然后利用一个集合，分别统计这些不同的$?^{\gcd(a,b)}+1,3-?\mod 2$的个数。可以发现这个集合的大小为$O(N)$。然后再代入$c$进行计算。

并且经过枚举，恰好发现$U(n)\%987898789$这个序列的周期为$T=987898788$。那么求$U(c^g+1)$就相当于求$U((c^g+1)\%T)$，求$U(n)$时使用矩阵快速幂算法即可。

本题由于模数比较特殊，可以避免使用矩阵快速幂进行计算。通过Mathematica用以下代码求$U(n)$
的递推式，发现为：

```Mathematica
RSolve[{a[n] == 10*a[n - 1] + a[n - 2], a[0] == 0, a[1] == 1}, a[n], n]
```

$$U(n)=\dfrac{(5+\sqrt{26})^n - (5-\sqrt{26})^n}{2\sqrt{26}}$$

并且，$26$恰好是模数$987898789$的[二次剩余](https://en.wikipedia.org/wiki/Quadratic_reciprocity)。可以计算出$\sqrt{26}\mod 987898789= 445663912$。

那么本题就不需要使用矩阵快速幂。只需要使用普通的快速幂算法进行计算即可，效率更高。并且，不需要先像上一种做法那样需要先枚举再确定周期。

## 代码

```C++
#include <bits/stdc++.h>
typedef long long ll;
using namespace std;
const int N=2000;
ll T=987898788,mod=987898789;
ll qpow(ll n,ll m,ll mod){
    ll a=1;
    for(;m;m>>=1){
        if(m&1) a=a*n%mod;
        n=n*n%mod;
    }
    return a;
}
void mul_self(ll b[2][2]){
    ll c[2][2]={0};
    for(int i=0;i<2;i++)
        for(int j=0;j<2;j++)
            for(int k=0;k<2;k++)
                c[i][j]=(c[i][j]+b[i][k]*b[k][j])%mod;
    memcpy(b,c,sizeof(c));
}
void mul(ll a[2],ll b[2][2]){
    ll c[2]={0};
    for(int i=0;i<2;i++)
        for(int k=0;k<2;k++)
            c[i]=(c[i]+a[k]*b[k][i])%mod;
    memcpy(a,c,sizeof(c));
}
ll a[2],b[2][2];
ll cal(ll n){
    a[0]=0,a[1]=1;
    b[0][0]=0;b[0][1]=b[1][0]=1;
    b[1][1]=10;
    for(;n;n>>=1){
        if(n&1) mul(a,b);
        mul_self(b);
    }
    return a[0];
}
int cnt[N+4];
int main(){
    for(int a=1;a<=N;a++){
        ++cnt[a];
        for(int b=a+1;b<=N;b++){
            int g=__gcd(a,b);
            if(a/g%2&&b/g%2) cnt[g]+=2;
            else cnt[0]+=2;
        }
    }
    ll ans=0;
    for(int c=1;c<=N;c++){
        ans=(ans+cal(c&1?2:1)*cnt[0])%mod;
        for(int g=1;g<=N;g++)
            ans=(ans+cal(qpow(c,g,T)+1)*cnt[g])%mod;
    }
    printf("%lld\n",ans);
}
```

```C++
#include <bits/stdc++.h>
typedef long long ll;
using namespace std;
const int N=2000;
ll mod=987898789;
ll qpow(ll n,ll m,ll mod){
    ll a=1;
    for(;m;m>>=1){
        if(m&1) a=a*n%mod;
        n=n*n%mod;
    }
    return a;
}
ll sqrt26=445663912;
ll inv2sqrt26=qpow(sqrt26*2,mod-2,mod);
ll cal(ll n){
    return (qpow(5+sqrt26,n,mod)-qpow(mod-sqrt26+5,n,mod)+mod)*inv2sqrt26%mod;
}
int cnt[N+4];
int main(){
    for(int a=1;a<=N;a++){
        ++cnt[a];
        for(int b=a+1;b<=N;b++){
            int g=__gcd(a,b);
            if(a/g%2&&b/g%2) cnt[g]+=2;
            else cnt[0]+=2;
        }
    }
    ll ans=0;
    for(int c=1;c<=N;c++){
        ans=(ans+cal(c&1?2:1)*cnt[0])%mod;
        for(int g=1;g<=N;g++)
            ans=(ans+cal(qpow(c,g,mod-1)+1)*cnt[g])%mod;
    }
    printf("%lld\n",ans);
}

```
