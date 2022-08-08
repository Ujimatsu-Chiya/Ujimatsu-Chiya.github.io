---
title: Project Euler 7
category:
  - Project Euler
tags:
mathjax: true
date: 2022-04-26 18:35:22
---

<escape><!-- more --></escape>

# Project Euler 7

## 题目

### 10001st prime

By listing the first six prime numbers: $2, 3, 5, 7, 11$, and $13$, we can see that the $6\mathrm{th}$ prime is $13$.

What is the $10 001\mathrm{st}$ prime number?

## 解决方案

使用sympy库中的prime函数计算即可。筛选素数的常见筛法有线性筛（时间复杂度$O(n)$）和埃氏筛。

埃氏筛的思想主要是标记所有合数。当遇到一个没有被标记过的数时，就认为它是质数，然后将这个质数的所有倍数全都标记为合数。因此，有一些合数会被它的所有质因数重复标记。

线性筛的思想则是需要维护一个数组v。这个数组v的含义是v[i]是i的最小的质因数。线性筛比埃氏筛
的效率高了一个对数级，因为其中的每个合数都只会被标记一次（被最小的质因数标记）。而数组v，则控制着每个数i不能利用比v[i]更大的质因数去重复标记其它合数。

两种筛法都可以用来计算积性函数。

## 代码

```Python
from sympy.ntheory.generate import prime

N = 10001
print(prime(N))
```

埃氏筛：

```Python
Q = 10001
pr = []
N = Q * len(bin(Q)) - 2
f = [0 for _ in range(N + 1)]
for i in range(2, N + 1):
    if f[i] == 0:
        pr.append(i)
        for j in range(i * i, N + 1, i):
            f[j] = 1

print(pr[Q - 1])
```
线性筛：

```C++
# include <bits/stdc++.h>
using namespace std;
const int Q=10001;
const int N=(1+log2(Q))*Q+4;
int v[N+4],pr[N+4],m=0;
int main(){
    for(int i=2;i<=N;i++){
        if(v[i]==0){
            v[i]=i;pr[++m]=i;
        }
        for(int j=1;j<=m;j++){
            if(pr[j]>v[i]||pr[j]>N/i)
                break;
            v[i*pr[j]]=pr[j];
        }
    }
    int ans=pr[Q];
    printf("%d\n",ans);
}

```