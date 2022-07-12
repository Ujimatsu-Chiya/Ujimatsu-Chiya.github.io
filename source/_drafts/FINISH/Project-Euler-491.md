---
title: Project Euler 491
tags:
  - Project Euler
  - 动态规划
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 491
## 题目
### Double pandigital number divisible by 11


We call a positive integer *double pandigital* if it uses all the digits $0$ to $9$ exactly twice (with no leading zero). For example, $40561817703823564929$ is one such number.

How many double pandigital numbers are divisible by $11$?




## 解决方案

这题由于涉及到数位的使用个数，因此考虑使用动态规划进行。

由于单个数位只使用$2$个，那么当前使用情况有$0,1,2$这三种情况，因此我们使用一个$10$位三进制数$b=b_9b_8\dots b_0$来表示当前数位的使用情况。

令$M=11$。令状态$f(b,j)(0< b< 3^{10},0<j<M)$表示构造的数中，已经使用的数位的情况为$i$，
模$M$为$j$的数的个数。

那么不难写出如下状态转移方程：

$$
f(i,j)=
\left \{\begin{aligned}
  &1  & & \mathrm{if\quad} \sum_{k=0}^9i_k=1\wedge i=3^j \\
  &0 & & \mathrm{else if\quad} \sum_{k=0}^9i_k=1 \\
  &\sum_{0<k<10,i_k>0,(10x+k)\%M=j} f(i-3^k,x) & & \mathrm{else}
\end{aligned}\right.
$$

方程的最后一行表示，从状态$f(i-3^k,x)$中的所有数右边都添加一个数位$k$，那么添加后数位使用情况就变成$i$，数的模$M$值就变成$(10x+k)\%M$。

最终答案为$f(3^{10}-1,0)$。

代码中的实现则为另一种方式，它是以“我为人人”的方式实现的，即将当前状态转移到所有的后继可能的状态。在本题中，这种写法会有效减少代码量。

## 代码

```C++
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const int D=10;
const int M=11;
const ll N=pow(3,D);
ll f[N][M];
int pw[D+1];
int main() {
    pw[0]=1;
    for(int i=1;i<=D;i++)
        pw[i]=pw[i-1]*3;
    for(int i=1;i<D;i++)
        f[pw[i]][i%M]++;
    for(int i=0;i<pw[D];i++)
        for(int j=0;j<M;j++)
            for(int k=0;k<D;k++)
                if(i/pw[k]%3<2)
                    f[i+pw[k]][(j*10+k)%M]+=f[i][j];
    ll ans=f[N-1][0];
    printf("%lld\n",ans);
}

```
