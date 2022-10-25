---
title: Project Euler 258
date: 2022-04-06 14:51:03
category:
  - Project Euler
tags:
mathjax: true
---
<escape><!-- more --></escape>

# Project Euler 258

## 题目

### A lagged Fibonacci sequence

A sequence is defined as:

- $g_k = 1$, for $0 \leq k \leq 1999$
- $g_k = g_{k-2000} + g_{k-1999}$, for $k \geq 2000$

Find $g_k \bmod 20092010$ for $k = 10^{18}$.

## 哈密顿-凯莱(Caylay-Camilton)定理

如果一个$n$阶矩阵$A$的特征多项式为$f(\lambda)=|A-\lambda I|=\sum_{i=0}^n b_i\lambda^i$，其中$b^i$为系数。那么矩阵多项式$f(A)=\sum_{i=0}^nb_iA^i$满足$f(A)=O$.

## 线性递推

对于一个线性递推$a_n=\sum_{j=1}^kc_ja_{n-j}$，可以构造如下矩阵进行$O(k^3\log n)$的线性递推计算：

$$
\begin{bmatrix}
c_1 & c_2 & c_3 &\cdots &c_{k-1} & c_k\\
1 & 0 & 0 & \cdots & 0 & 0\\
0 & 1 & 0 & \cdots & 0 & 0\\
\vdots & \vdots & \vdots & \ddots & \vdots & \vdots\\
0 & 0 & 0 &\cdots & 0 & 0\\
0 & 0 & 0 &\cdots & 1 & 0
\end{bmatrix}
\begin{bmatrix}
a_{n-1}\\
a_{n-2}\\
a_{n-3}\\
\vdots\\
a_{n-k+1}\\
a_{n-k}
\end{bmatrix}
=
\begin{bmatrix}
a_n\\
a_{n-1}\\
a_{n-2}\\
\vdots\\
a_{n-k+2}\\
a_{n-k+1}
\end{bmatrix}
$$

令$A=\begin{bmatrix}
c_1 & c_2 & c_3 &\cdots &c_{k-1} & c_k\\
1 & 0 & 0 & \cdots & 0 & 0\\
0 & 1 & 0 & \cdots & 0 & 0\\
\vdots & \vdots & \vdots & \ddots & \vdots & \vdots\\
0 & 0 & 0 &\cdots & 0 & 0\\
0 & 0 & 0 &\cdots & 1 & 0
\end{bmatrix},x=
\begin{bmatrix}
a_{k-1}\\
a_{k-2}\\
a_{k-3}\\
\vdots\\
a_1\\
a_0
\end{bmatrix}$

## 解决方案

可以知道，矩阵$A$的特征多项式为$f(\lambda)=|A-\lambda I|=\lambda^k-(\sum_{j=1}^k c_j \lambda^{k-j})$。

代入Caylay-Camilton定理，可以发现，$A^k=\sum_{j=1}^k c_j A^{k-j}$。

由题目可知$A^{2000}=A+I$。

Caylay-Camilton定理说明，任意$m\geq k$的矩阵幂$A^k$都可以表示成一个为$\sum_{i=0}^{k-1} v_iA^i$的矩阵多项式，其中$v_i$为系数。

而为了求$a_n$，可以计算$A^nx$，然后取向量$A^nx$的最后一个值$(A^nx)_{k-1}$即可。

那么令$A^n=\sum_{i=0}^{k-1} v_iA^i$。

可以知道，$A^nx=\sum_{i=0}^{k-1} v_iA^ix$。

系数$v_i$可以通过快速幂算法进行多项式卷积进行计算，然后将卷积结果系数大于等于$k$的部分通过矩阵多项式回退到小于$k$。

最终结果为$a_n=\sum_{i=0}^{k-1} v_i\cdot a_i$

原因：容易发现，计算$Ax$只是将整个向量$x$向下平移了一次，新的值将在向量$x$上面填充。

因此，不必要将整个向量$A^ix$计算出来，只需要将最后一个值$(A^ix)_{k-1}$计算出来，并与系数相乘即可，因为此时的$i$不会发生$i\geq k$的情况。

## 代码

```C++
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;

const int M=2000;
ll N=1e18;
ll mod = 20092010;
ll a[M];
ll p[M];
ll b[M];
ll ans_mat[M];
void mul_ploy(ll a[M],ll b[M],ll p[M]){
    //做的是乘法，对应的就是多项式系数的卷积。
    ll c[M<<1];memset(c,0,sizeof(c));
    for(int i=0;i<M;i++)
        for(int j=0;j<M;j++)
            c[i+j]=(c[i+j]+a[i]*b[j])%mod;
    //利用递推式F(A)的值，将>=M的所有临时系数转化成<M的系数。
    for(int i=M*2-1;i>=M;i--)
        for(int j=0;j<M;j++)
            c[i-M+j]=(c[i-M+j]+c[i]*p[j]);
    for(int i=0;i<M;i++)
        a[i]=c[i];
}
int main(){
    // a代表递推式的前M个值
    for(int i=0;i<M;i++)
        a[i]=1;
    // p代表Hamilton-Cayley而来的矩阵多项式的系数，题中为F(A)=A^2000=A+I
    p[0]=p[1]=1;
    // b代表A^(2^i)时所有的A^(2^i)=sum from j=0 to M-1 A^j*b_j时系数b_j的值。
    b[1]=1;
    ans_mat[0]=1;
    for(;N;N>>=1){
        if(N&1) mul_ploy(ans_mat,b,p);
        mul_ploy(b,b,p);
    }
    ll ans=0;
    //需要注意的是，当向量和一个矩阵相乘后，我们只要向量中的第一个值。因为向量乘一次这个矩阵递推式，那么所有值都会前移一次。
    for(int i=0;i<M;i++)
        ans=(ans+ans_mat[i]*a[i])%mod;
    printf("%lld\n",ans);
}
```
