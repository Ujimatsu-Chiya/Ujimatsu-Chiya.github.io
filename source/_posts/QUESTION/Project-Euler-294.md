---
title: Project Euler 294
tags:
  - Project Euler
  - 动态规划
  - 矩阵快速幂+
mathjax: true
date: 2022-07-06 13:08:10
---

<escape><!-- more --></escape>

# Project Euler 294

## 题目

### Sum of digits - experience #23

For a positive integer $k$, define $d(k)$ as the sum of the digits of $k$ in its usual decimal representation. Thus $d(42) = 4+2 = 6$.

For a positive integer $n$, define $S(n)$ as the number of positive integers $k < 10^n$ with the following properties :

- $k$ is divisible by $23$ and
- $d(k) = 23$.

You are given that $S(9) = 263626$ and $S(42) = 6377168878570056$.

Find $S(11^{12})$ and give your answer mod $10^9$.

## 解决方案

不难想到使用动态规划解决本题。

令$N=11^{12},M=23,O=23.$假设状态$f(i,j,k)(1\le i\le N,0\le j< M,0\le k\le O)$表示目前所有$i$位**带前导**$0$的**非负整数**中，模$M$为$j$，数位和为$k$的所有数之和。那么不难写出如下状态转移方程：

$$
f(i,j,k)=
\left \{\begin{aligned}
  &1  & & \mathrm{if\quad} i=1,0\le i=j\le \min(9,O) \\
  &0 & & \mathrm{else if\quad} i=1 \\
  &\sum_{d=0}^{\min(9,k)}\sum_{0\le x<M,(10x+d)\%M=j} f(i-1,x,k-d) & & \mathrm{else}
\end{aligned}\right.
$$

其中，最后一条式子的意思是考虑在状态$f(i-1,x,k-d)$中的每一个数后面添加一个数位$d$，添加之后那么其对$M$的取模值就变成了$(10x+d)\%M$，数位和也变成了$k$。

若盲目按照这个方程进行转移，由于$N$非常大，时间复杂度明显是不可接受的。

考虑使用矩阵快速幂进行改善。定义一个转移矩阵$A$，其中这个矩阵的边长为$M(O+1)$，每一个对应下标值$i$的行和列都被编码成一个状态，用两个数$(a_i,b_i)(0\le a_i< M,0\le b_i\le O)$表示。其中$a_i$表示当前的数模$M$的值，$b_i$表示当前的数的数位之和。

如果存在$0\le d<10$，使得($10a_i+d)\%M=a_j\wedge b_i+d=b_j$，那么$A_{ij}=1$，否则$A_{ij}=0$。定义好矩阵$A$后直接通过矩阵快速幂加速转移。此时的时间复杂度为$O(M^3\cdot O^3\cdot \log N)$.时间比起直接求$f$有进步，但依然非常慢。

更进一步的改进：如果我们已经求出了$f(a,\cdot,\cdot)$和$f(b,\cdot,\cdot)$中的所有值，我们可以以$O(M^2\cdot N^2)$求出$f(a+b,\cdot,\cdot)$的所有值。

枚举所有$f(a,i,j)$和$f(b,x,y)$，那么就将这两部分值合并起来：

$f(a,i,j)\cdot f(b,x,y)\rightarrow f(a+b,i\cdot 10^{b}+b,j+y)$

我们将$f(a,\cdot,\cdot)$中的所有数都乘上一个$10^b$，然后加上$b$位数的所有情况，两部分一一互相拼接，最终就形成了$f(a+b,\cdot,\cdot)$，在这个过程中，需要维护好拼接之后的数模$M$的值，以及它们的数位之和。

因此，这给了我们一个方案：依次求出$f(2^0,\cdot,\cdot),f(2^1,\cdot,\cdot),f(2^2,\cdot,\cdot),\dots$。然后针对$N$，选择这些求出的$f(2^i,\cdot,\cdot)$进行合并即可。这种做法的时间复杂度为$O(M^2\cdot N^2\cdot \log n)$，降低了次数阶。

## 代码

```C++
# include <bits/stdc++.h>
using namespace std;
typedef long long ll;
ll N=pow(11,12);
const int M=23;
const int O=23;
ll mod=1000000000;
ll fp[104][M+1][O+1],f[M+1][O+1];
void cal(ll dest[M+1][O+1],ll a[M+1][O+1],ll b[M+1][O+1],int pw){
    ll c[M+1][O+1]={0};
    for(int i=0;i<M;i++)
        for(int j=0;j<M;j++)
            for(int k=0;k<=O;k++)
                for(int l=0;k+l<=O;l++){
                    c[(pw*i+j)%M][k+l]+=a[i][k]*b[j][l];
                    c[(pw*i+j)%M][k+l]%=mod;
                }
    memcpy(dest,c,sizeof(c));
}
int main(){
    for(int i=0;i<=min(9,O);i++)
        fp[0][i][i]=f[i][i]=1;
    int pw=10;
    for(ll n=N-1,i=0;n;n>>=1,i++){
        if(n&1) cal(f,f,fp[i],pw);
        cal(fp[i+1],fp[i],fp[i],pw);
        pw=pw*pw%M;
    }
    ll ans=f[0][O];
    printf("%lld\n",ans);
}

```
