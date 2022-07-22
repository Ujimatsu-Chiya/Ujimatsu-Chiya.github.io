---
title: Project Euler 509
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 509
## 题目
### Divisor Nim



Anton and Bertrand love to play three pile Nim.<br />
However, after a lot of games of Nim they got bored and changed the rules somewhat.<br />
They may only take a number of stones from a pile that is a <dfn title="a proper divisor of n is a divisor of n smaller than n">proper divisor</dfn> of the number of stones present in the pile.<br /> E.g. if a pile at a certain moment contains 24 stones they may take only 1,2,3,4,6,8 or 12 stones from that pile.<br />
So if a pile contains one stone they can't take the last stone from it as 1 isn't a proper divisor of 1.<br />
The first player that can't make a valid move loses the game.<br />
Of course both Anton and Bertrand play optimally.

The triple (<var>a</var>,<var>b</var>,<var>c</var>) indicates the number of stones in the three piles.<br />
Let <var>S</var>(<var>n</var>) be the number of winning positions for the next player for 1 \le <var>a</var>, <var>b</var>, <var>c</var> \le <var>n</var>.<br /><var>S</var>(10) = 692 and <var>S</var>(100) = 735494.

Find <var>S</var>(123456787654321) modulo 1234567890.



# Project Euler 509
## 题目
### Divisor Nim

Anton and Bertrand love to play three pile Nim.<br>However, after a lot of games of Nim they got bored and changed the rules somewhat.<br>They may only take a number of stones from a pile that is a <dfn title="a proper divisor of n is a divisor of n smaller than n">proper divisor</dfn> of the number of stones present in the pile.<br>E.g. if a pile at a certain moment contains 24 stones they may take only 1,2,3,4,6,8 or 12 stones from that pile.<br>So if a pile contains one stone they can’t take the last stone from it as 1 isn’t a proper divisor of 1.<br>The first player that can’t make a valid move loses the game.<br>Of course both Anton and Bertrand play optimally.
The triple (a,b,c) indicates the number of stones in the three piles.<br>Let S(n) be the number of winning positions for the next player for 1 \le a, b, c \le n.<br>S(10) = 692 and S(100) = 735494.<br>Find S(123456787654321) modulo 1234567890.


## 解决方案

[A007814](https://oeis.org/A007814)

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