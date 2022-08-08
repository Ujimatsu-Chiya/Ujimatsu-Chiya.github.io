---
title: Project Euler 284
category:
  - Project Euler
tags:
mathjax: true
date: 2022-08-05 21:41:01
---

<escape><!-- more --></escape>

# Project Euler 284

## 题目

### Steady Squares

The $3$-digit number $376$ in the decimal numbering system is an example of numbers with the special property that its square ends with the same digits: $376^2 = 141376$. Let's call a number with this property a steady square.

Steady squares can also be observed in other numbering systems. In the base $14$ numbering system, the $3$-digit number $c37$ is also a steady square: $c37^2 = aa0c37$, and the sum of its digits is $c+3+7=18$ in the same numbering system. The letters $a, b, c$ and $d$ are used for the $10, 11, 12$ and $13$ digits respectively, in a manner similar to the hexadecimal numbering system.

For $1 \le n \le 9$, the sum of the digits of all the $n$-digit steady squares in the base $14$ numbering system is $2d8$ ($582$ decimal). Steady squares with leading $0$'s are not allowed.

Find the sum of the digits of all the n-digit steady squares in the base $14$ numbering system for $1 \le n \le 10000$ (decimal) and give your answer in the base $14$ system using lower case letters where necessary.

## 解决方案

不难发现，如果一个$n$位$14$进制数是满足题意，那么它满足以下方程：

$$a^2\equiv a(\mod 14^n)$$

可以将其重新写成$a^2-a\equiv0(\mod 14^n)$。并且，方程的两个解$x_n,y_n$将会满足$x_n+y_n=14^n+1$，并且两个解的个位分别为$7$和$8$。因此，一对解中，除了其最低位之和为$15$，所有的对应位之和为$13$。根据中国剩余定理，不失一般性，假设$x_n\equiv 1(\mod 2^n),x_n\equiv0(\mod 7^n)$。

通过进一步打表可以发现，在方程$a^2-a\equiv0(\mod 14^n)$的两个解的最高位中再添加一位，即可变成方程$a^2-a\equiv0(\mod 14^{n+1})$的解$x_{n+1},y_{n+1}$。

令这个数位为$d$。那么令$x_{n+1}=14^nd + x_n$，并且有$x_{n+1}^2\equiv x_{n+1}(\mod 14^{n+1})$

联立后，得到$14^{2n}d^2+2\cdot 14^nd\cdot x_n+x_n^2\equiv14^nd+x_n(\mod 14^{n+1})$

最终，左边第一项明显是$14^{n+1}$的倍数；对于第二项，由于$x_n\equiv0(\mod 7^n)$，因此第二项也是$14^{n+1}$的倍数。

因此，方程最终化成：

$$d\equiv\dfrac{x_n^2-x_n}{14^n}(\mod 14)$$

因此将计算出的$d$拼接在$x_n$的最高位，形成$x_{n+1}$。

最终直接统计即可。

## 代码

本题使用了GMP库进行大整数运算。

```C++
#include <bits/stdc++.h>
#include<gmpxx.h>
using namespace std;
typedef long long ll;


const int N=10000,B=14;
string to_B(mpz_class a){
    string s;
    for(;a;a/=B){
        mpz_class b=a.get_si()%B;
        int x=b.get_si();
        if(x<10) s+=char('0'+x);
        else s+=char('a'+x-10);
    }
    reverse(s.begin(),s.end());
    return s;
}
int f(int now){
    int ans=1;
    int d=now,s=0;
    mpz_class x=0,pw=1,t;
    for(int n=1;n<=N;n++){
        s+=d;
        if(d==0) ans+=n*(B-1)+2-s;
        else if(d==B-1) ans+=s;
        else ans+=n*(B-1)+2;
        x+=pw*d;pw*=B;
        t=x*(x-1)/pw%B;
        d=t.get_si();
    }
    return ans;
}
int main() {
    string ans=to_B(f(B/2));
    cout<<ans<<endl;
}

```
