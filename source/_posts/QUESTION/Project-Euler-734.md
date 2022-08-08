---
title: Project Euler 734
category:
  - Project Euler
tags:
  - 快速沃尔什变换
  - 动态规划
mathjax: true
date: 2022-08-05 21:41:44
---

<escape><!-- more --></escape>

# Project Euler 734

## 题目

### A bit of prime

The *logical-OR* of two bits is $0$ if both bits are $0$, otherwise it is $1$.

The *bitwise-OR* of two positive integers performs a <i>logical OR</i> operation on each pair of corresponding bits in the binary expansion of its inputs.

For example, the bitwise-OR of $10$ and $6$ is $14$ because $10 = 1010_2$, $6 = 0110_2$ and $14 = 1110_2$.

Let $T(n, k)$ be the number of $k$-tuples $(x_1, x_2,\cdots,x_k)$ such that

- every $x_i$ is a prime $\leq n$
- the bitwise-OR of the tuple is a prime $\leq n$

For example, $T(5, 2)=5$. The five $2$-tuples are $(2, 2), (2, 3), (3, 2), (3, 3)$ and $(5, 5)$.

You are given $T(100, 3) = 3355$ and $T(1000, 10) \equiv 2071632 \pmod{1\,000\,000\,007}$

Find $T(10^6,999983)$. Give your answer modulo $1\,000\,000\,007$

## 解决方案

令$N=10^6,Q=999983$，一开始不难想到使用动态规划解决本问题。

令$P$为$N$以内的质数集合。令$f(i,j)(1\le i\le Q,j\ge 0)$表示当前长度为$i$的序列中，有多少种填入质数$p$的方法，使得整个序列的或运算结果为$j$。不难写出如下状态转移方程：

$$
f(i,j)=
\left \{\begin{aligned}
  &1 & & \mathrm{if\quad} i=1\wedge j\in P \\
  &0 & & \mathrm{else if\quad} i=1 \\
  &\sum_{p\in P}\sum_{k|p=j} f(i-1,k) & & \mathrm{else}
\end{aligned}\right.
$$

但是，对于$Q$这种数据范围而言，直接进行转移效率非常低。

如果我们已经求出了长度为$a$的序列的各种填法$f(a,\cdot)$和长度为$b$的各种填法$f(b,\cdot)$，不难知道我们可以通过卷积组合出$f(a+b,\cdot)$。

枚举所有的$f(a,i)$和$f(b,j)$，将这两部分值直接合并起来：

$g(a,i)\cdot g(b,j)\rightarrow g(a+b,i|j)$

直接枚举这两部分的值效率非常低，可以使用快速沃尔什变换加速计算这两部分的合并。

因此，这给了我们一个方案：依次求出$f(2^0,\cdot),f(2^1,\cdot),f(2^2,\cdot),\dots$。然后针对$Q$，选择这些求出的$f(2^i,\cdot)$进行合并即可。

最终答案为

$$\sum_{p\in P}f(Q,p)$$

## 代码

```C++
#include <bits/stdc++.h>
# include "tools.h"
using namespace std;
typedef long long ll;

const int N=1000000;
const int M=999983;
int mod = 1000000007;

int pr[N/5+100],v[N+4],m=0;
int main(){
    for(int i=2;i<=N;i++){
        if(v[i]==0){
            pr[++m]=i;v[i]=m;
        }
        for(int j=1;j<=m;j++){
            if(j>v[i]||pr[j]>N/i) break;
            v[i*pr[j]]=j;
        }
    }
    vector<int>b(N+1);
    for(int i=1;i<=m;i++)
        b[pr[i]]=1;
    fwt.init_mod(mod);
    vector<int>a=fwt.powOr(b,M);
    int ans=0;
    for(int i=1;i<=m;i++)
        ans=(ans+a[pr[i]])%mod;
    printf("%d\n",ans);
}

```
