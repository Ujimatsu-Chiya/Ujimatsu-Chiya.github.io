---
title: Project Euler 662
category:
  - Project Euler
tags:
  - 动态规划
mathjax: true
date: 2022-06-22 23:27:16
---

<escape><!-- more --></escape>

# Project Euler 662

## 题目

### Fibonacci paths

Alice walks on a lattice grid. She can step from one lattice point $A (a,b)$ to another $B (a+x,b+y)$ providing distance $AB = \sqrt{x^2+y^2}$ is a Fibonacci number $\{1,2,3,5,8,13,\ldots\}$ and $x\ge 0,$  $y\ge 0$.

In the lattice grid below Alice can step from the blue point to any of the red points.

![](../images/p662_fibonacciwalks.png)

Let $F(W,H)$ be the number of paths Alice can take from $(0,0)$ to $(W,H)$.

You are given $F(3,4) = 278$ and $F(10,10) = 215846462$.

Find $F(10\,000,10\,000) \bmod 1\,000\,000\,007$.

## 解决方案

这道题目可以使用非常直接的动态规划思想解决。

那么假设$N=M=10000$首先可以将所有移动单次移动步骤$(x,y)$预处理出来，其中$x^2+y^2$是一个斐波那契数，$x^2+y^2\le N^2+M^2$，在这个数据范围下，一共有$D=88$个移动步骤。

令状态$f(i,j)(0\le i\le N,0\le j\le M)$为从点$(0,0)$到点$(i,j)$的路线数量，那么不难写出如下状态转移方程：

$$f(i,j)=
\left \{\begin{aligned}
  &1  & & \text{if\quad} i=0\land j=0 \\
  &\sum_{x,y,x\le i,y\le j} f(i-x,j-y)& & \text{else}
\end{aligned}\right.
$$

那么最终答案就是$f(N,M)$。

但是，直接用代码描述这个方程的转移过程会非常慢，因为时间复杂度为$O(N\cdot M\cdot D)$，运行过程极慢。

以下对程序的优化参考了Thread的一些内容。

观察上面的过程，可以发现，直接进行状态转移时，依次访问的位置$f(i-x,j-y)$是毫无顺序的，这时内存的访问并不连续。非顺序访存将导致程序效率大大降低（如缓存总是被刷新等等）。

那么，将数组每一列进行错开，数组中，以$f[i+j][i]$表示状态$f(i,j)$的值。转移时，先枚举坐标之和$t=i+j$，再枚举某个方向$(x,y)$，然后从坐标之和为$t-x-y$处的点**按顺序**转移到坐标之和为$t$的点，从而达到顺序访存的目的（具体实现见代码）。

## 代码

这份代码是优化之前的，速度比较慢。

```C++
#include <bits/stdc++.h>
# define pi pair<int,int>
typedef long long ll;
using namespace std;
const int N=10000,M=10000;
vector<pi>v;
vector<int>fib;
ll f[N+M+1][M+1],mod=1e9+7;
int main(){
    int a=1,b=2;
    for(;a*a<=N*N+M*M;){
        int c=a+b;
        fib.push_back(a);
        a=b;b=c;
    }
    for(int d:fib){
        for(int x=0;x<=N&&x*x<=d*d;x++){
            int y=int(sqrt(d*d-x*x)+1e-9);
            if(y<=M&&x*x+y*y==d*d){
                v.push_back(pi(x,y));
            }
        }
    }
    sort(v.begin(),v.end());
    f[0][0]=1;
    for(int i=0;i<=N;i++)
        for(int j=0;j<=M;j++){
            if(i==0&&j==0) continue;
            if(i>j&&i<=M) f[i][j]=f[j][i];
            else{
                for(auto &[dx,dy]:v){
                    if(dx>i) break;
                    if(dy<=j){
                        f[i][j]+=f[i-dx][j-dy];
                        if(f[i][j]>=mod) f[i][j]-=mod;
                    }
                }
            }
        }
    ll ans=f[N][M];
    printf("%lld\n",ans);
}

```

这份代码是优化之后的，运行时间大概是原来的$\dfrac{1}{4}$。

```C++
#include <bits/stdc++.h>
# define pi pair<int,int>
typedef long long ll;
using namespace std;
const int N=10000,M=10000;
vector<pi>v;
vector<int>fib;
ll f[N+M+1][M+1],mod=1e9+7;
int main(){
    int a=1,b=2;
    for(;a*a<=N*N+M*M;){
        int c=a+b;
        fib.push_back(a);
        a=b;b=c;
    }
    for(int d:fib){
        for(int x=0;x<=N&&x*x<=d*d;x++){
            int y=int(sqrt(d*d-x*x)+1e-9);
            if(y<=M&&x*x+y*y==d*d){
                v.push_back(pi(x,y));
            }
        }
    }
    f[0][0]=1;
    for(int t=0;t<=N+M;t++){
        int x_min=max(0,t-M),x_max=min(N,t);
        for(auto &[dx,dy]:v){
            int s=t-dx-dy;
            if(s<0) continue;
            for(int j=max(dx,x_min);j<=x_max;j++)
                f[t][j]+=f[s][j-dx];
        }
        for(int j=x_min;j<=x_max;j++)
            f[t][j]%=mod;
    }
    ll ans=f[N+M][N];
    printf("%lld\n",ans);
}

```
