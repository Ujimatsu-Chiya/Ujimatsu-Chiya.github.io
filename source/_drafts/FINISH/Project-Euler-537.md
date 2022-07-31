---
title: Project Euler 537
tags:
  - Project Euler
  - 动态规划
  - 快速数论变换
mathjax: true
---
<escape><!-- more --></escape>





# Project Euler 537
## 题目
### Counting tuples

Let $\pi(x)$ be the prime counting function, i.e. the number of prime numbers less than or equal to $x$.

For example, $\pi(1)=0, \pi(2)=1, \pi(100)=25$.

Let $T(n,k)$ be the number of $k$-tuples $(x_1,\dots,x_k)$ which satisfy:

- every $x_i$ is a positive integer;
- $\displaystyle \sum_{i=1}^k \pi(x_i)=n$

For example $T(3,3)=19$.

The $19$ tuples are 

$\begin{aligned}
& (1,1,5), (1,5,1), (5,1,1), (1,1,6), (1,6,1), (6,1,1), (1,2,3), \\
& (1,3,2), (2,1,3), (2,3,1), (3,1,2), (3,2,1), (1,2,4), (1,4,2), \\
& (2,1,4), (2,4,1), (4,1,2), (4,2,1), (2,2,2).
\end{aligned}$

You are given $T(10,10) = 869 985$ and $T(10^3,10^3) ≡ 578 270 566 (\mod 1 004 535 809)$.

Find $T(20 000, 20 000) \mod 1 004 535 809$.


## 解决方案

令$N=M=20000,P=1004535809$。考虑使用动态规划计算$T$。

用$c[i]$表示$\pi$序列中有多少个$n$为$\pi(n)=i$。不难写出关于$T$的状态转移方程：

$$
T(i,j)=
\left \{\begin{aligned}
  &1 & & \mathrm{if\quad} i=0\wedge j=0 \\
  &0 & & \mathrm{else if\quad} i=0 \\
  &\sum_{k=0}^j T(i-1,j-k) \cdot c[k] & & \mathrm{else}
\end{aligned}\right.
$$

最后一行方程表示在状态$T(i-1,j-k)$中的序列填一个数，它的$\pi$函数值中有$c[k]$个是$k$，从而达到状态$T(i,j)$。

不过直接进行转移效率非常低。

如果我们已经求出了长度为$a$的序列的各种填法$T(a,\cdot)$和长度为$b$的各种填法$T(b,\cdot)$，不难知道我们可以通过卷积组合出$T(a+b,\cdot)$。

枚举所有的$T(a,i)$和$T(b,j)$，将这两部分值直接合并起来：

$T(a,i)\cdot T(b,j)\rightarrow T(a+b,i+j)$

直接枚举这两部分的值效率非常低，可以使用[快速数论变换](https://en.wikipedia.org/wiki/Discrete_Fourier_transform_over_a_ring#Number-theoretic_transform)加速计算这两部分的合并。快速数论变换最基本的用途就是用来求多项式模上的卷积，将$O(n^2)$的时间复杂度下降到$O(n\log n)$。

因此，这给了我们一个方案：依次求出$Tg(2^0,\cdot),T(2^1,\cdot),T(2^2,\cdot),\dots$。然后针对$Q$，选择这些求出的$T(2^i,\cdot)$进行合并即可。


## 代码


```C++
#include <bits/stdc++.h>
#include "tools.h"
using namespace std;
typedef long long ll;

const int N=20000,M=20000;
int g=3,mod=1004535809;

const int O=log(N)*N*2+4;
int v[O+4],pr[O/10+1000],m=0;
int main(){
    ntt.init(g,mod);
    for(int i=2;i<=O;i++){
        if(v[i]==0){
            v[i]=i;pr[++m]=i;
        }
        for(int j=1;j<=O;j++){
            if(pr[j]>v[i]||pr[j]>O/i) break;
            v[i*pr[j]]=pr[j];
        }
    }
    vector<int>a{1},b(N+1);
    b[0]=1;
    for(int i=1;i<=N;i++)
        b[i]=pr[i+1]-pr[i];
    for(int m=M;m;m>>=1){
        if(m&1) a=ntt.cal(a,b);
        b=ntt.cal(b,b);
        a.resize(N+1);
        b.resize(N+1);
    }
    int ans=a[N];
    printf("%d\n",ans);
}

```