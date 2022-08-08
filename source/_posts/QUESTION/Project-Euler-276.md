---
title: Project Euler 276
category:
  - Project Euler
tags:
  - OEIS
  - 数论分块
mathjax: true
date: 2022-07-27 23:49:40
---

<escape><!-- more --></escape>

# Project Euler 276

## 题目

### Primitive Triangles

Consider the triangles with integer sides $a, b$ and $c$ with $a \le b \le c$.

An integer sided triangle $(a,b,c)$ is called primitive if $\gcd(a,b,c)=1,(\gcd(a,b,c)=\gcd(a,\gcd(b,c)))$.

How many primitive integer sided triangles exist with a perimeter not exceeding $10 000 000$?

## 解决方案

首先考虑这个问题的一个简单版：

去除互质的限制后，有多少个三角形？

暴力枚举出一部分项后，查询OEIS，结果为[A001400](https://oeis.org/A001400)，找到FORMULA一栏，它给出了一个$9$阶的递推式：

```
a(n) = 1 + (a(n-2) + a(n-3) + a(n-4)) - (a(n-5) + a(n-6) + a(n-7)) + a(n-9). - Norman J. Meluch (norm(AT)iss.gm.com), Mar 09 2000
```

那么，令去除掉互质限制后的周长不超过$n$的三角形个数为$f(n)$，令$g(n)$表示原本题目中要求的三角形个数。

每一个互质的三角形，每条边的边长都延长到原来的$k$倍，那么它的周长也将延长到原来的$k$倍。每一个非互质三角形都对应着一个互质三角形。因此，可以写出$f$和$g$之间的关系：

$$f(n)=\sum_{k=1}^n g(\lfloor\dfrac{n}{k}\rfloor)$$

其中$k$就是不同的倍数。那么就可以写成关于$g(n)$的递推式：

$$g(n)=f(n)-\sum_{k=1}^n g(\lfloor\dfrac{n}{k}\rfloor)$$

右边的式子是一个明显的数论分块特征，最终使用数论分块来完成$g(n)$的计算。

## 代码

```C++
#include <bits/stdc++.h>
typedef long long ll;
typedef unsigned long long ull;
using namespace std;
const int N=1e7;
ull f[N+4]={0,0,0,1,1,2,3,5,6,9,11,15};
ull g[N+4];
ull cal(int n){
    if(n<=2) return 0;
    if(g[n]!=0) return g[n];
    ull ans=f[n];
    for(int l=2,r;l<=n;l=r+1){
        r=n/(n/l);
        ans-=cal(n/l)*(r-l+1);
    }
    return g[n]=ans;
}
int main(){
    for(int n=12;n<=N;n++)
        f[n]=(f[n-2]+f[n-3]+f[n-4])-(f[n-5]+f[n-6]+f[n-7])+f[n-9]+1;
    ull ans=cal(N);
    printf("%llu\n",ans);
}

```
