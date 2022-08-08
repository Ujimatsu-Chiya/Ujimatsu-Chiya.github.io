---
title: Project Euler 222
category:
  - Project Euler
tags:
  - 动态规划
mathjax: true
date: 2022-06-05 09:29:23
---

<escape><!-- more --></escape>

# Project Euler 222

## 题目

### Sphere Packing

What is the length of the shortest pipe, of internal radius $50\mathrm{mm}$, that can fully contain $21$ balls of radii $30\mathrm{mm}, 31\mathrm{mm}, \dots, 50\mathrm{mm}$?

Give your answer in micrometres ($10^{-6} \text{ m}$) rounded to the nearest integer.

## 解决方案

由于每个球的直径都大于管内的半径，因此每一个球在管内最多和两个球相切。如图：

![](../images/p222-1.png)

那么，如果半径为$r_2$的球放在$r_1$的球上面，并且管内的直径为$d$，那么它们的球心的高度之差可以由下面的公式给出（根据勾股定理即可推出）：

$$g(r_1,r_2)=\sqrt{(r_1+r_2)^2-(r_1+r_2-d)^2}$$

由于每个球放进去时，它只和最上面的球接触。这启发我们使用状态压缩动态规划解决这个问题。

假设一共有$n$个球，第$i$个球的半径为$r_i$，用一个$n$比特数$b=b_{n-1}b_{n-2}\dots b_0$表示球体的使用情况，那么令$f(i,j)(0\le i<2^n,0\le j< n,i_j=1)$表示当前使用的球的情况个数为$i$，放在最高的球为$j$时，当前最高的球的圆心最矮有多高，那么可以列出以下状态转移方程：

$$
f(i,j)=
\left \{\begin{aligned}
  &r_j  & & \mathrm{if\quad} i=2^j \\
  &\min_{0\le k<n,(i\oplus 2^j)_{k}=1} f(i\oplus 2^k,k)+g(r_k,r_j) & & \mathrm{else}
\end{aligned}\right.
$$

那么，最终答案需要对$f$加回最高的那个球的半径，为：

$$\min_{i=0}^n f(2^n-1,i)+r_i$$

顺带一提的是，最终答案的方法打印出来是这个样子：

$$[49, 47, 45, 43, 41, 39, 37, 35, 33, 31, 30, 32, 34, 36, 38, 40, 42, 44, 46, 48, 50]$$

这是一个很有规律的模式，不过我尚未有证明这个模式的能力。

## 代码

```C++
#include <bits/stdc++.h>
using namespace std;
const int M=21;
double D=50;
double f[1<<M][M],g[M][M];
int r[M];
int main(){
    for(int i=0;i<M;i++)
        r[i]=30+i;
    D*=2;
    memset(f,0x4f,sizeof(f));
    for(int i=0;i<M;i++)
        f[1<<i][i]=r[i];
    for(int i=0;i<M;i++)
        for(int j=i+1;j<M;j++){
            double d0=r[i]+r[j],d1=r[j]+r[i]-D;
            g[i][j]=g[j][i]=sqrt(d0*d0-d1*d1);
        }
    for(int s=1;s<(1<<M);s++){
        for(int i=0;i<M;i++){
            for(int j=0;j<M;j++){
                if((s>>j&1)==0)
                    f[s|1<<j][j]=min(f[s|1<<j][j],f[s][i]+g[i][j]);
            }
        }
    }
    double ans=1e10;
    for(int i=0;i<M;i++)
        ans=min(ans,f[(1<<M)-1][i]+r[i]);
    ans *= 1000;
    printf("%.f\n",ans);
}

```
