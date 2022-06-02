---
title: Project Euler 251
tags:
  - Project Euler
mathjax: true
date: 2022-06-02 21:04:14
---

<escape><!-- more --></escape>

# Project Euler 251

## 题目

### Cardano Triplets

A triplet of positive integers $(a,b,c)$ is called a Cardano Triplet if it satisfies the condition:

$$\sqrt[3]{a + b \sqrt{c}} + \sqrt[3]{a - b \sqrt{c}} = 1$$

For example, $(2,1,5)$ is a Cardano Triplet.

There exist $149$ Cardano Triplets for which $a+b+c \le 1000$.

Find how many Cardano Triplets exist such that $a+b+c \le 110,000,000$.

## 解决方案

本解决方案参考了Thread的内容。

先将整个方程去除根号：

1. 等式两边立方，整理后得

$$2a+3\sqrt[3]{a^2-b^2c}\cdot(\sqrt[3]{a + b \sqrt{c}} + \sqrt[3]{a - b \sqrt{c}})=1$$

2. 代入原来的$\sqrt[3]{a + b \sqrt{c}} + \sqrt[3]{a - b \sqrt{c}}=1$，移项后，整理得：

$$2a-1=-3\sqrt[3]{a^2-b^2c}$$

3. 等式两边再取立方，整理后得：

$$8a^3+15a^2+6a-1=27b^2c\qquad(1)$$

原式等价于求$8a^3+15a^2+6a-1=27b^2c$的解。

左边的式子可以分解为$(a+1)^2(8a-1)$，不难发现，只有当$a$满足$a\equiv 2(\mod 3)$时，$3|(a+1)^2(8a-1)$。

因此，令$a=3k+2,k\ge0$，将此式代回$(1)$，整理后，问题转化为求有多少个三元组$(k,b,c)$，满足以下方程：

$$(k+1)^2(8k+5)=b^2c\qquad (2)$$

其中，$k\ge0,b>0,c>0,3k+2+b+c\le N,N=110000000$。

观察到$(2)$两侧都是一个平方项乘以一个一次项，令$g=\gcd(k+1,b)$，那么令$p,q$满足$k+1=gp,b=gq$，其中$\gcd(p,q)=1$。那么将$p,q$代入$(2)$，有

$$p^2(8k+5)=q^2c\qquad(3)$$

由于$\gcd(p,q)=1$，因此存在$m$，使得$c=mp^2,8k+5=mq^2$。

联立$a=3k+2,b=gq,c=mp^2,k+1=gp,8k+5=mq^2$，可将问题转化为如下形式：
有多少个整数三元组$(a=3gp-1,b=gq,c=mp^2)$满足以下条件：

1. $\gcd(p,q)=1$
2. $8gp=mq^2+3$
3. $3gp+gq+mp^2\le N+1$
4. $p,q,g,m>0$

我们可以枚举每对互质的$(p,q)$后进行统计。使用扩展欧几里得算法来计算出条件$2$的$g,m$值，假设一对最小正整数解为$(g_0,m_0)$，那么这个方程的通解为$g'=tq^2+g_0,m'=8tp+m_0$，其中$t\ge 0$。最终，将通解代入条件$3$，那么$t$满足$t(q^3+3pq^2+8p^3)+g_0q+m_0p^2+3g_0p\le N+1$。统计满足条件的所有$t$的个数。

## 代码

```C++
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const ll N = 110000000;
ll ex_gcd(ll a,ll b,ll &x,ll &y){
    if(b==0){
        x=1;y=0;return a;
    }
    ll g=ex_gcd(b,a%b,x,y);
    ll z=x-(a/b)*y;
    x=y;y=z;return g;
}
//解不定方程ax+my=c。
ll congruence(ll a,ll c,ll m,ll &x,ll &y) {
    ll g = ex_gcd(a, m, x, y);
    if (c % g != 0) return -1;
    ll mc = c / g;
    ll ma = abs(a / g);
    y *= mc;
    y = (y % ma + ma) % ma;
    x = (c - m * y) / a;
    return abs(g);
}
int main(){
    ll g,m;
    //两个上限暂时还没证明出怎么来的。
    ll mxQ = sqrt(((N+1)/3*8-3)/5)+3;
    ll mxP = sqrt((N+1)/5)+3;
    ll ans=0;
    for(ll q=1;q<=mxQ;q+=2){
        for(ll p=1;p<=mxP&&q*q*3+p*p*8+q*8<=N*8-1;p++){
            if(congruence(p*8,3,-q*q,g,m) != 1)
                continue;
            ll s = g*q+m*p*p+g*p*3,d = q*q*q+p*q*q*3+p*p*p*8;
            ans += (s <= N + 1 ? (N+1-s)/d+1:0);
        }
    }
    printf("%lld\n",ans);
}

```
