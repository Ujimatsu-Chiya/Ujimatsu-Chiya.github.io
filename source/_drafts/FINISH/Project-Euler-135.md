---
title: Project Euler 135
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    


# Project Euler 135
## 题目
### Same differences
Given the positive integers, $x, y$, and $z$, are consecutive terms of an arithmetic progression, the least value of the positive integer, $n$, for which the equation, $x^2 − y^2 − z^2 = n$, has exactly two solutions is $n = 27$:

$$34^2 − 27^2 − 20^2 = 12^2 − 9^2 − 6^2 = 27$$

It turns out that $n = 1155$ is the least value which has exactly ten solutions.

How many values of $n$ less than one million have exactly ten distinct solutions?


## 解决方案

$x,y,z$是一个等差数列，并且由于$n>0$，因此只有当$x>y>z$时，才会有$x^2-y^2-z^2>0$。

因此设公差为$d$，那么有$(z+2d)^2-(z+d)^2-z^2=n$。

将方程左边化简，并分解因式，有$(3d-z)(d+z)=n$。

故在枚举方程的解过程中，先枚举$z$的值，再枚举$d$的值，注意$d$的值要从$\lfloor\dfrac{d}{3}\rfloor+1$开始枚起来，这样才能保证一开始的$n$的正数。


## 代码

```C++
# include <bits/stdc++.h>
using namespace std;
const int N=1e6,Q=10;
int c[N+4];
int main(){
    for(int z=1;z<=N;z++){
        for(int d=z/3+1;;d++){
            int w=(3*d-z)*(d+z);
            if(w>=N) break;
            c[w]+=1;
        }
    }
    int ans=0;
    for(int i=1;i<=N;i++)
        if(c[i]==Q) ++ans;
    printf("%d\n",ans);
}

```