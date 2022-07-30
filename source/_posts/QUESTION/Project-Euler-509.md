---
title: Project Euler 509
tags:
  - Project Euler
  - SG定理
mathjax: true
date: 2022-07-27 23:50:55
---

<escape><!-- more --></escape>

# Project Euler 509

## 题目

### Divisor Nim

Anton and Bertrand love to play three pile Nim.

However, after a lot of games of Nim they got bored and changed the rules somewhat.

They may only take a number of stones from a pile that is a <dfn title="a proper divisor of n is a divisor of n smaller than n">proper divisor</dfn> of the number of stones present in the pile.

E.g. if a pile at a certain moment contains $24$ stones they may take only $1,2,3,4,6,8$ or $12$ stones from that pile.

So if a pile contains one stone they can't take the last stone from it as $1$ isn't a proper divisor of $1$.

The first player that can't make a valid move loses the game.
Of course both Anton and Bertrand play optimally.

The triple $(a,b,c)$ indicates the number of stones in the three piles.

Let $S(n)$ be the number of winning positions for the next player for $1 \le a, b, c \le n$.

$S(10) = 692$ and $S(100) = 735494$.

Find $S(123456787654321)\text{ modulo }1234567890$.

## 解决方案

在每一次操作中，一方可以拿起三堆石头$(a,b,c)$的其中一堆的石头的因数个。并且这$3$堆石头是相互独立的。因此，三堆石头的$sg$函数$sg(a,b,c)=sg(a)\oplus sg(b)\oplus sg(c)$.那么此时只需要单独考虑一堆石头的情况$sg(n)$。

只拿一堆石头时，不难写出$sg(n)$为：

$$
sg(n)=
\left \{\begin{aligned}
  &0 & & \mathrm{if\quad} n=1 \\
  &\text{mex}(\{sg(n-d)|(d \mid n)\wedge d\neq n \}) & & \mathrm{else}
\end{aligned}\right.
$$

其中运算$\text{mex}(s)$表示集合$s$中未出现的最小的非负整数。

那么通过以下程序暴力打印出一部分数的$sg$函数值，在OEIS中查询后结果为[A007814](https://oeis.org/A007814)。

```C++
#include <bits/stdc++.h>
# include "tools.h"
using namespace std;
typedef long long ll;
const int N=100,M=100;
int sg[N+4];
bool mex[M+4];
int main(){
    sg[1]=0;
    for(int i=2;i<=N;i++){
        memset(mex,0,sizeof(mex));
        vector<ll>d=divisors(i);
        d.pop_back();
        for(ll x:d)
            mex[sg[i-x]]=1;
        int j=0;
        for(;mex[j];++j);
        sg[i]=j;
        printf("%d %d\n",i,sg[i]);
    }
}

```

这个数列说明$sg(n)$是最大的正整数$k$使得$2^k|n$。

那么不难计算得到，$1\sim N$中有$\lfloor\dfrac{N}{2^i}\rfloor-\lfloor\dfrac{N}{2^{i+1}}\rfloor$个数，其$sg$函数值为$i$。

因此，最终直接三重循环枚举$sg$值，直接求个数之积的和。

## 代码

```C++
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const ll N=123456787654321;
const int M=60;
ll cnt[M+4],mod=1234567890;
int main(){
    for(int i=0;i<=M;i++)
        cnt[i]=((N>>i)-(N>>(i+1)))%mod;
    ll ans=0;
    for(int i=0;i<=M;i++)
        for(int j=0;j<=M;j++)
            for(int k=0;k<=M;k++)
                if(i^j^k) ans=(ans+cnt[i]*cnt[j]%mod*cnt[k])%mod;
    printf("%lld\n",ans);
}

```
