---
title: Project Euler 236
category:
  - Project Euler
tags:
mathjax: true
date: 2022-07-01 17:37:03
---

<escape><!-- more --></escape>

# Project Euler 236

## 题目

### Luxury Hampers

Suppliers ‘A’ and ‘B’ provided the following numbers of products for the luxury hamper market:

|Product|‘A’|‘B’|
|-|-|-|
|Beluga Caviar|$5248$|$640$|
|Christmas Cake|$1312$|$1888$|
|Gammon Joint|$2624$|$3776$|
|Vintage Port|$5760$|$3776$|
|Champagne Truffles|$3936$|$5664$|

Although the suppliers try very hard to ship their goods in perfect condition, there is inevitably some spoilage - *i.e.* products gone bad.
The suppliers compare their performance using two types of statistic:

- The five *per-product spoilage rates* for each supplier are equal to the number of products gone bad divided by the number of products supplied, for each of the five products in turn.

- The *overall spoilage rate* for each supplier is equal to the total number of products gone bad divided by the total number of products provided by that supplier.

To their surprise, the suppliers found that each of the five per-product spoilage rates was worse (higher) for ‘B’ than for ‘A’ by the same factor (ratio of spoilage rates), $m>1$; and yet, paradoxically, the overall spoilage rate was worse for ‘A’ than for ‘B’, also by a factor of $m$.

There are thirty-five $m>1$ for which this surprising result could have occurred, the smallest of which is $1476/1475$.

What’s the largest possible value of $m$?

Give your answer as a fraction reduced to its lowest terms, in the form $u/v$.

## 解决方案

假设$m=\dfrac{u}{v}$，$\gcd(u,v)=1$，$a_1,a_2,\dots,a_5$分别是$A$店铺对应$5$个商品的损耗量，$b_1,b_2,\dots,b_5$同理。

那么可以写出以下几个等式：

$$\dfrac{b_1}{a_1}=\dfrac{5u}{41v}=\dfrac{u_1}{v_1},\dfrac{b_2}{a_2}=\dfrac{b_3}{a_3}=\dfrac {b_5}{a_5}=\dfrac{59u}{41v}=\dfrac{u_2}{v_2},\dfrac{b_4}{a_4}=\dfrac{59u}{90v}=\dfrac{u_4}{v_4}$$

其中，$\gcd(u_j,v_j)=1,j\in\{1,2,4\}$。

根据最后一个条件：A点的损耗总数为B的$m$倍，那么可以写出：

$$\dfrac{\sum_{i=1}^5a_i}{\sum_{i=1}^5b_i}=\dfrac{295u}{246v}=\dfrac{U}{V}\qquad(1)$$

其中$\gcd(U,V)=1$.

我们可以考虑枚举$a_2,b_2$的所有值，求出所有可能的二元组$\dfrac{u}{v}$。一个可能的$\dfrac{u}{v}$就可以确定所有比值$\dfrac{u_j}{v_j}$和$\dfrac{U}{V}$。根据这些比值，倒推出所有可能的$(a_i,b_i)$出来，$(a_i,b_i)$的可能取值有$(v_j,u_j),(2v_j,2u_j),(3v_j,3u_j),\dots$。枚举的时候，注意$(a_i,b_i)$不能超过原来的上限。

可以发现，$(a_2,b_2),(a_3,b_3),(a_5,b_5)$具有相同的比值，因此可以将它们统一考虑。

那么，对于每对$(u,v)$，现在考虑下面关于$k_1,k_2,k_4$的方程的解：

$$\dfrac{k_1v_1+k_2v_2+k_4v_4}{k_1u_1+k_2u_2+k_4u_4}=\dfrac{U}{V}$$

这个方程可以写成：

$$k_1(v_1V-u_1U)+k_2(v_2V-u_2U)+k_4(v_4V-u_4U)=0$$

其中$k_1,k_4>0,k_2\ge 3$。如果找到了一组解$(k_1,k_2,k_4)$，那么说明$\dfrac{u}{v}$是一个可能的$m$。

由于$k_1,k_2,k_4$的上限都很低，因此可以直接进行二重循环的枚举，当然也可以进行一次循环且使用扩展欧几里得算法解决。

## 代码

```C++
# include <bits/stdc++.h>
# define pi pair<int,int>
typedef long long ll;
using namespace std;
bool ok(ll c1,ll c2,ll c3,ll k1,ll k2,ll k3){
    for(int i=1;i<=k1;i++){
        for(int j=1;j<=k3;j++){
            ll x=-c1*i-c3*j;
            if(x%c2) continue;
            x/=c2;
            if(3<=x&&x<=k2) return 1;
        }
    }
    return 0;
}
int main(){
    set<pi>st;
    for(int a2=1;a2<=1312;a2++){
        for(int b2=1;b2<=1888;b2++){
            if(__gcd(a2,b2)!=1) continue;
            int u=41*b2,v=59*a2;
            if(u<=v) continue;
            int g=__gcd(u,v);
            u/=g;v/=g;
            int u1=5*u,v1=41*v;
            g=__gcd(u1,v1);
            u1/=g;v1/=g;
            int u2=59*u,v2=41*v;
            g=__gcd(u2,v2);
            u2/=g;v2/=g;
            int u4=59*u,v4=90*v;
            g=__gcd(u4,v4);
            u4/=g;v4/=g;
            int U=295*u,V=246*v;
            g=__gcd(U,V);
            U/=g;V/=g;
            ll k1=min(5248/v1,640/u1),k2=min(1312*6/v2,1888*6/u2),k4=min(5760/v4,3776/u4);
            if(k1==0||k2==0||k4==0) continue;
            if(ok(v1*V-u1*U,v2*V-u2*U,v4*V-u4*U,k1,k2,k4)) st.insert(pi(u,v));
        }
    }
    string ans;
    double mx=0;
    for(auto &[u,v]:st){
        double d=1.0*u/v;
        if(d>mx) ans=to_string(u)+"/"+to_string(v),mx=d;
    }
    cout<<ans<<endl;
}

```
