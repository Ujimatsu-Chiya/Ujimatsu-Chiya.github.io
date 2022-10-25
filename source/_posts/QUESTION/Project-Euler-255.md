---
title: Project Euler 255
category:
  - Project Euler
tags:
mathjax: true
date: 2022-07-27 23:50:59
---

<escape><!-- more --></escape>

# Project Euler 255

## 题目

### Rounded Square Roots

We define the *rounded-square-root* of a positive integer n as the square root of n rounded to the nearest integer.

The following procedure (essentially Heron's method adapted to integer arithmetic) finds the rounded-square-root of $n$:

Let $d$ be the number of digits of the number $n$.

If $d$ is odd, set $x_0 = 2 \times 10^{(d-1)/2}$.

If $d$ is even, set $x_0 = 7 \times 10^{(d-2)/2}$.

Repeat:

$$x_{k+1} = \Biggl\lfloor{\dfrac{x_k + \lceil{n / x_k}\rceil}{2}}\Biggr\rfloor$$

until $x_{k+1} = x_k$.

As an example, let us find the rounded-square-root of $n = 4321$.

$n$ has $4$ digits, so $x_0 = 7 \times 10^{(4-2)/2} = 70$.
$$x_1 = \Biggl\lfloor{\dfrac{70 + \lceil{4321 / 70}\rceil}{2}}\Biggr\rfloor = 66$$
$$x_2 = \Biggl\lfloor{\dfrac{66 + \lceil{4321 / 66}\rceil}{2}}\Biggr\rfloor = 66$$

Since $x_2 = x_1$, we stop here.

So, after just two iterations, we have found that the rounded-square-root of $4321$ is $66$ (the actual square root is $65.7343137\dots$).

The number of iterations required when using this method is surprisingly low.<br />
For example, we can find the rounded-square-root of a $5$-digit integer $(10,000 \le n \le 99,999)$ with an average of $3.2102888889$ iterations (the average value was rounded to $10$ decimal places).

Using the procedure described above, what is the average number of iterations required to find the rounded-square-root of a $14$-digit number $(10^{13} \le n < 10^{14})$?

Give your answer rounded to $10$ decimal places.

Note: The symbols $\lfloor x \rfloor$ and $\lceil x \rceil$ represent the <dfn title="the largest integer not greater than x">floor function</dfn> and <dfn title="the smallest integer not less than x">ceiling function</dfn> respectively.

## 解决方案

令$N=14$。

实际上，$x_0$相对比较接近$\sqrt{n}$。注意到迭代算法$\lceil n/x_k\rceil$的一项，因此从第一步迭代起，$n$从$10^{N-1}$到$ 10^N-1$，这几个数就按照这个值$\lceil n/x_0\rceil$的不同被划分成$O(\sqrt{10^{N/2}})$个连续的区间。接下来对同一个区间里面的数一起进行第一次迭代（注意这轮区间内迭代的结果都相同），然后一起进入下一轮。

为了方便实现，整个迭代过程的模拟使用深度优先搜索。

## 代码

```C++
#include <bits/stdc++.h>
typedef long long ll;
using namespace std;
const int N=14;
const ll x0=N&1?pow(10,(N-1)>>1)*2:pow(10,(N-2)>>1)*7;
ll cnt=0;
void dfs(int f,ll v,ll l,ll r){
    cnt+=r-l+1;
    for(ll x=l,y=min(r,(l+v-1)/v*v);x<=r;x=y+1,y=min(x+v-1,r)){
        ll w=((x+v-1)/v+v)>>1;
        if(w==v) continue;
        dfs(f+1,w,x,y);
    }
}
int main(){
    ll l=pow(10,N-1),r=pow(10,N)-1;
    dfs(1,x0,l,r);
    double ans=1.0*cnt/(r-l+1);
    printf("%.10f\n",ans);
}
```
