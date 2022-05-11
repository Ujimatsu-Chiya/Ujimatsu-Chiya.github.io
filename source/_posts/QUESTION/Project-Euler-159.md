---
title: Project Euler 159
tags:
  - Project Euler
  - 动态规划
mathjax: true
date: 2022-05-11 19:28:07
---

<escape><!-- more --></escape>

# Project Euler 159

## 题目

### Digital root sums of factorisations

A composite number can be factored many different ways. For instance, not including multiplication by one, $24$ can be factored in $7$ distinct ways:

$\begin{aligned}
24 &= 2\times2\times2\times3 \\
24 &= 2\times3\times4 \\
24 &= 2\times2\times6 \\
24 &= 4\times6 \\
24 &= 3\times8\\
24 &= 2\times12\\
24 &= 24
\end{aligned}$

Recall that the digital root of a number, in base $10$, is found by adding together the digits of that number, and repeating that process until a number is arrived at that is less than $10$. Thus the digital root of $467$ is $8$.

We shall call a Digital Root Sum (DRS) the sum of the digital roots of the individual factors of our number.

The chart below demonstrates all of the DRS values for $24$.

|Factorisation|Digital Root Sum|
|-|-|
|$2 \times2 \times2 \times3$|$9$|
|$2 \times3 \times4$|$9$|
|$2 \times2 \times6$|$10$|
|$4 \times6$|$10$|
|$3 \times8$|$11$|
|$2 \times12$|$5$|
|$24$|$6$|

The maximum Digital Root Sum of $24$ is $11$.

The function $\mathrm{mdrs}(n)$ gives the maximum Digital Root Sum of $n$. So $\mathrm{mdrs}(24)=11$.

Find $\sum \mathrm{mdrs}(n)$ for $1 < n < 1,000,000$.

## 解决方案

可以证明，数根的值$r(x)=(x-1)\%9+1$，也就是当$x$为$9$的倍数时，$r(x)=9$，否则$r(x)=x\%9$。特别的，$r(0)=0$。

由于任意一个$k$位十进制数$d=d_{k-1}...d_2d_1d_0$都可以写成如下形式的多项式：

$$d=\sum_{i=0}^{k=1}d_i 10^i$$

因此，假设$s(d)$为$d$的数位和，那么有：

$$s(d)=\sum_{i=0}^{k-1}d_i\equiv \sum_{i=0}^{k-1}d_i10^i(\mod 10)$$

这说明，数位和的值$s(d)$和数本身的值$d$关于$9$同余。因此进行有限次操作后，最终得到的一位数的数字根一定和原来的数关于同余。由于正数的数位和一定大于$0$，因此有$r(x)=(x-1)\%9+1$。

回到本题，通过类似埃氏筛法的思想，对于每个数$n$，用一个集合$D_n$存储$n$的除了$1$和$n$以外的所有不大于$\sqrt{n}$的因子，。

基于动态规划的思想，可以想到，将每个数$i$拆成两个非平凡因子（即不为$1$或$n$）$d$和$\dfrac{i}{d}$的乘积。那么，$\mathrm{mdrs}(d)+\mathrm{mdrs}(\dfrac{i}{d})$有可能成为$\mathrm{mdrs}(i)$。

设$f(i)=\mathrm{mdrs(i)}(i\ge 1)$。因此，可以列出如下状态转移方程：

$$
f(i)=
\left \{\begin{aligned}
  &1  & & \mathrm{if\quad} i=1 \\
  &\max(r(i),\max_{d\in D_i}\{f(d)+f(\dfrac{i}{d})\})  & & \mathrm{else}
\end{aligned}\right.
$$

最终答案为$\sum_{i=2}^{N-1}f(i)$。

## 代码

```C++
# include <bits/stdc++.h>
using namespace std;
const int N=1000000;
typedef long long ll;
vector<int>g[N+4];
int f[N+4];
int fun(int x){
    return x%9?x%9:9;
}
int main(){
    for(int i=2;i<N;i++){
        for(ll j=1ll*i*i;j<=N;j+=i)
            g[j].push_back(i);
    }
    int ans=0;
    for(int i=2;i<N;i++){
        f[i]=fun(i);
        for(int x:g[i])
            f[i]=max(f[i],f[x]+f[i/x]);
        ans+=f[i];
    }
    printf("%d\n",ans);
}

```
