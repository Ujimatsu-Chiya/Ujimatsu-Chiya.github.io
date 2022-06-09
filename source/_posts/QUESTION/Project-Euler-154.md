---
title: Project Euler 154
tags:
  - Project Euler
mathjax: true
date: 2022-05-11 19:27:51
---

<escape><!-- more --></escape>

# Project Euler 154

## 题目

### Exploring Pascal's pyramid

A triangular pyramid is constructed using spherical balls so that each ball rests on exactly three balls of the next lower level.

![](../images/p154_pyramid.png)

Then, we calculate the number of paths leading from the apex to each position:

A path starts at the apex and progresses downwards to any of the three spheres directly below the current position.

Consequently, the number of paths to reach a certain position is the sum of the numbers immediately above it (depending on the position, there are up to three numbers above it).

The result is *Pascal’s pyramid* and the numbers at each level n are the coefficients of the trinomial expansion  $(x + y + z)^n$.

How many coefficients in the expansion of $(x + y + z)^{200000}$ are multiples of $10^{12}$?

## 解决方案

[多项式定理](https://en.wikipedia.org/wiki/Multinomial_theorem)是二项式定理的扩展。这里我们使用其三项式的形式。

因此，将$(x+y+z)^n$展开后，有：

$$(x+y+z)^n=\sum_{i=0}^n\sum_{j=0}^{n-i}C_n^iC_{n-i}^jx^iy^jz^{n-i-j}$$

其中，明显可以看出，$C_n^iC_{n-i}^j=\dfrac{n!}{i!j!(n-i-j)!}$。

预先计算$i!(0\le i\le n)$中分别有多少个质因数$2,5$。然后直接枚举每个项的系数，根据这个三项式系数的定义式判断是否有$12$个质因子$2$和$12$个质因子$5$。

不过，由于多项式中的项$x,y,z$是无序的，因此可以通过假定$x,y,z$的次数$i,j,n-i-j$满足$i\le j\le n-i-j$，减少枚举量。

## 代码

```C++
# include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N=200000;
const int B=12;

int f2[N+4],f5[N+4];
int c2=B,c5=B;
void solve(int w,int &c2,int &c5){
    c2=c5=0;
    for(;w%2==0;w/=2,++c2);
    for(;w%5==0;w/=5,++c5);
}
int main(){
    for(int i=2,c2,c5;i<=N;i++){
        solve(i,c2,c5);
        f2[i]=f2[i-1]+c2;
        f5[i]=f5[i-1]+c5;
    }
    ll ans=0;
    for(int i=0;i*3<=N;i++){
        if(i%1000==0)
            printf("%d\n",i);
        for(int j=i;j+j<=N-i;j++){
            int k=N-i-j;
            int cnt2=f2[N]-f2[i]-f2[j]-f2[k],cnt5=f5[N]-f5[i]-f5[j]-f5[k];
            if(cnt2>=c2&&cnt5>=c5){
                if(i==j&&j==k) ++ans;
                else if(i==j||j==k) ans+=3;
                else ans+=6;
            }
        }
    }
    printf("%lld\n",ans);
}

```
