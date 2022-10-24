---
title: Project Euler 141
category:
  - Project Euler
tags:
mathjax: true
date: 2022-05-10 13:47:22
---

<escape><!-- more --></escape>

# Project Euler 141

## 题目

### Investigating progressive numbers, n, which are also square

A positive integer, $n$, is divided by $d$ and the quotient and remainder are $q$ and $r$ respectively. In addition $d, q$, and $r$ are consecutive positive integer terms in a geometric sequence, but not necessarily in that order.

For example, $58$ divided by $6$ has quotient $9$ and remainder $4$. It can also be seen that $4, 6, 9$ are consecutive terms in a geometric sequence (common ratio $\dfrac{3}{2}$).

We will call such numbers, $n$, progressive.

Some progressive numbers, such as $9$ and $10404 = 102^2$, happen to also be perfect squares.

The sum of all progressive perfect squares below one hundred thousand is $124657$.

Find the sum of all progressive perfect squares below one trillion ($10^{12}$).

## 解决方案

按照题意，有等式$n=qd+r$，其中$r< q$是可以确定的.

那么假设$d< q$（因为无论$q<d$还是$q>d$，对上面$n$的结果不会有任何改变。），并且这个公比是一个有理数，由最简分数$\dfrac{a}{b}$表示，那么有

$d=\dfrac{a}{b} \cdot r,q=\dfrac{a^2}{b^2}\cdot r$

如果$q$是一个正整数，那么$b^2\mid r$。因此就存在一个$c$，使得$r=cb^2$。

此时$d=abc,q=a^2c$。

那么$n=qd+r=a^3bc^2+b^2c$。

枚举这三个数$a,b,c$即可，要保证$\gcd(a,b)=1,a>b$。

## 代码

```C++
# include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const ll N=1e12;
unordered_set<ll>st1,st;
int main(){
    for(ll i=1;i*i<N;i++)
        st1.insert(i*i);
    for(ll a=2,a3;(a3=a*a*a)<N;a++){
        ll d=2-a%2;
        for(ll b=1;b<a&&b*(a3+b)<N;b+=d){
            if(__gcd(a,b)==1){
                for(ll c=1,w;(w=b*c*(b+a3*c))<N;c++){
                    if(st1.count(w))
                        st.insert(w);
                }
            }
        }
    }
    ll ans=0;
    printf("%lld\n",ans);
}

```
