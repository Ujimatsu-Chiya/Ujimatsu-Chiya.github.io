---
title: Project Euler 461
category:
  - Project Euler
tags:
  - meet-in-the-middle
mathjax: true
date: 2022-07-13 22:57:23
---

<escape><!-- more --></escape>

# Project Euler 461

## 题目

### Almost Pi

Let $f_n(k)=e^{\frac{k}{n}}-1$, for all non-negative integers $k$.

Remarkably, $f_{200}(6)+f_{200}(75)+f_{200}(89)+f_{200}(226)= \underline{3.1415926}44529\dots\approx \pi$.

In fact, it is the best approximation of $\pi$ of the form $f_n(a)+f_n(b)+f_n(c)+f_n(d)$ for $n=200$.

Let $g(n)=a^2+b^2+c^2+d^2$ for $a, b, c, d$ that minimize the error: $|f_n(a)+f_n(b)+f_n(c)+f_n(d)-\pi|$ (where $|x|$ denotes the absolute value of $x$).

You are given $g(200)=6^2+75^2+89^2+226^2=64658$.

Find $g(10000)$.

## 解决方案

可以看到，题中使用了$4$个$f_n(i)$进行逼近，那么我们考虑将这$4$个$f_n(i)$分成两对，然后使用meet-in-the-middle算法进行求解。

1. 先将所有$f_n(i)$枚举并计算出来，注意计算到的$f_n(i)>\pi$时，停止枚举。

2. 将以上的$f_n(i)+f_n(j)(i\le j)$枚举出来。当枚举到$f_n(i)+f_n(j)>\pi$ 时，停止枚举。并记录所有的$(f_n(i)+f_n(j),i^2+j^2)$二元组，存在数组$p$中。

3. 将$p$中按照第一关键字进行排序。这一步骤是算法中耗时最长的一部分。

4. 通过双指针法遍历数组$p$，找出最优的解。

使用`C++`内置的`pair`比较慢，因此实现时重新自定义了一个结构体，整体效率大概增加了$\dfrac{1}{3}$。

## 代码

```C++
#include <bits/stdc++.h>
using namespace std;
const int N=10000;
double e=exp(1),pi=acos(-1.0);
struct P{
    double x;
    int id;
    bool operator < (const P &p) const{
        return x<p.x;
    }
}pa[N*N];
double f[N+N];
int m=0,n=0;
int main(){
    double pi=acos(-1);
    double mx=log(pi+1);
    for(int i=0;i<N+N;i++){
        double e=1.0*i/N;
        f[m++]=exp(e)-1;
        if(e>mx) break;
    }
    for(int i=0;i<m;i++)
        for(int j=0;j<=i;j++){
            double w=f[i]+f[j];
            pa[n++]=P{w,i*i+j*j};
            if(w>pi) break;
        }
    sort(pa,pa+n);
    double eps=1e9;
    int ans=0;
    for(int l=0,r=n-1;l<n;l++){
        for(;r>=0&&pa[l].x+pa[r].x>pi;--r);
        if(r>0){
            double w=abs(pi-pa[l].x-pa[r].x);
            if(w<eps){
                eps=w;ans=pa[l].id+pa[r].id;
            }
        }
        if(r+1<n){
            double w=abs(pi-pa[l].x-pa[r+1].x);
            if(w<eps){
                eps=w;ans=pa[l].id+pa[r+1].id;
            }
        }
    }
    printf("%d\n",ans);
}

```
