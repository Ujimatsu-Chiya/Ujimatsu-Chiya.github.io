---
title: Project Euler 511
tags:
  - Project Euler
  - 动态规划
  - 矩阵快速幂&#43;
mathjax: true
date: 2022-07-13 22:57:47
---

<escape><!-- more --></escape>

# Project Euler 511

## 题目

### Sequences with nice divisibility properties

Let $\text{Seq}(n,k)$ be the number of positive-integer sequences $\{a_i\}_{1\le i\le n}$ of length $n$ such that:

- $n$ is divisible by $a_i$ for $1\le i\le n$, and
- $n + a_1 + a_2 + \dots + a_n$ is divisible by $k$.

Examples:
$\text{Seq}(3,4) = 4$, and the $4$ sequences are:

$\begin{aligned}
\{1, 1, 3\} \\
\{1, 3, 1\} \\
\{3, 1, 1\} \\
\{3, 3, 3\}
\end{aligned}$

$\text{Seq}(4,11) = 8$, and the $8$ sequences are:

$\begin{aligned}
\{1, 1, 1, 4\}\\
\{1, 1, 4, 1\}\\
\{1, 4, 1, 1\}\\
\{4, 1, 1, 1\}\\
\{2, 2, 2, 1\}\\
\{2, 2, 1, 2\}\\
\{2, 1, 2, 2\}\\
\{1, 2, 2, 2\}\\
\end{aligned}$

The last nine digits of $\text{Seq}(1111,24)$ are $840643584$.

Find the last nine digits of $\text{Seq}(1234567898765,4321)$.

## 解决方案

注意到第$2$个条件中的式子可以看成是$(a_1+1)+(a_2+1)+\dots+(a_n+1)$。因此在第$1$个条件时，处理完$n$的所有因子后，全部加$1$，那么第$2$个条件就可以转化成条件$a_1'+a_2'+\dots+a_n'$是$k$的倍数。

假设$S$是经过第$1$个条件的限定后，可以填入序列$a'$的数的集合。

那么，不难想到使用动态规划来解决本题。令$N=1234567898765,M=4321$。假设状态$f(i,j)(0\le i\le N,0<j<M)$是长度为$n$的序列中，有多少种填法使得序列$a'$的元素之和模$M$为$j$。那么不难写出状态转移方程为：

$$
f(i,j)=
\left \{\begin{aligned}
  &1  & & \mathrm{if\quad} i=0\wedge j=0 \\
  &0 & & \mathrm{else if\quad} i=0 \\
  &\sum_{x\in S}f(i-1,(j-x)\%M) & & \mathrm{else}
\end{aligned}\right.
$$

但是，对于$N$这种数据范围而言，直接进行转移效率非常低。如果直接使用矩阵快速幂，那么矩阵的边长长达$M$，仍然不可接受。

如果我们已经求出了长度为$a$的序列的各种填法$f(a,\cdot)$和长度为$b$的各种填法$f(b,\cdot)$，不难知道我们可以通过$O(M^2)$的时间复杂度组合出$f(a+b,\cdot)$。

枚举所有的$f(a,i)$和$f(b,j)$，将这两部分值直接合并起来：

$f(a,i)\cdot f(b,j)\rightarrow f(a+b,(i+j)\%M)$

因此，这给了我们一个方案：依次求出$f(2^0,\cdot),f(2^1,\cdot),f(2^2,\cdot),\dots$。然后针对$N$，选择这些求出的$f(2^i,\cdot,\cdot)$进行合并即可。这种做法的时间复杂度为$O(M^2\cdot \log N)$。

## 代码

```C++
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const ll N=1234567898765,M=4321;
ll mod=1e9;
ll cnt[M];
ll a[M],b[M];
void getd(ll N){
    for(ll i=1;i*i<=N;i++)
    if(N%i==0){
        ++cnt[(i+1)%M];
        if(i*i!=N) ++cnt[(N/i+1)%M];
    }
}
void cal(ll a[M],ll b[M],ll ans[M]){
    ll c[M]={0};
    for(int i=0;i<M;i++)
        for(int j=0;j<M;j++)
            c[(i+j)%M]=(c[(i+j)%M]+a[i]*b[j])%mod;
    memcpy(ans,c,sizeof(c));
}
int main(){
    getd(N);
    a[0]=1;
    memcpy(b,cnt,sizeof(b));
    for(ll M=N;M;M>>=1){
        if(M&1) cal(a,b,a);
        cal(b,b,b);
    }
    printf("%lld\n",a[0]);
}

```
