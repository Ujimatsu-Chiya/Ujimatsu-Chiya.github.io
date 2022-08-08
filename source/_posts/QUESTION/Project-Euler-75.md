---
title: Project Euler 75
category:
  - Project Euler
tags:
mathjax: true
date: 2022-05-02 16:36:30
---

<escape><!-- more --></escape>

# Project Euler 75

## 题目

### Singular integer right triangles

It turns out that $12 \mathrm{cm}$ is the smallest length of wire that can be bent to form an integer sided right angle triangle in exactly one way, but there are many more examples.

$\begin{aligned}
& \mathbf{12cm}: (3,4,5) \\
& \mathbf{24cm}: (6,8,10) \\
& \mathbf{30cm}: (5,12,13) \\
& \mathbf{36cm}: (9,12,15) \\
& \mathbf{40cm}: (8,15,17) \\
& \mathbf{48cm}: (12,16,20)
\end{aligned}$

In contrast, some lengths of wire, like $20 \mathrm{cm}$, cannot be bent to form an integer sided right angle triangle, and other lengths allow more than one solution to be found; for example, using $120 \mathrm{cm}$ it is possible to form exactly three different integer sided right angle triangles.

$$\mathbf{120cm}: (30,40,50), (20,48,52), (24,45,51)$$

Given that $L$ is the length of the wire, for how many values of $L \leq 1,500,000$ can exactly one integer sided right angle triangle be formed?

## 本原勾股数组

[本原](https://mathworld.wolfram.com/PrimitivePythagoreanTriple.html)[勾股数组](https://mathworld.wolfram.com/PythagoreanTriple.html)，即一个正整数三元组$(a,b,c)$，满足$a^2+b^2+c^2\wedge\gcd(a,b,c)=1$。

通过枚举一系列的二元组$(s,t)$，其中$s>t\geq 1\wedge\gcd(s,t)=1,s,t$为奇数，可以不重不漏地产生本原勾股数组$(st,\dfrac{s^2-t^2}{2},\dfrac{s^2+t^2}{2})$。

## 解决方案

使用上面的方法枚举本原勾股数组$(a,b,c)$，再将其对应的非本原勾股数组$(ka,kb,kc)(k>1)$一一枚举出，统计对应周长下的直角三角形个数。

## 代码

```C++
# include <bits/stdc++.h>
using namespace std;
const int N=1500000;
int d[N+4];
int main(){
    for(int s=1;s+s*s<=N;s+=2)
    for(int t=1;t<s;t+=2){
        if(__gcd(s,t)!=1) continue;
        int a=s*t,b=(s*s-t*t)/2,c=(s*s+t*t)/2;
        int s=a+b+c;
        for(int k=s;k<=N;k+=s)
            ++d[k];
    }
    int ans=0;
    for(int i=1;i<=N;i++)
        ans+=(d[i]==1);
    printf("%d\n",ans);
}

```
