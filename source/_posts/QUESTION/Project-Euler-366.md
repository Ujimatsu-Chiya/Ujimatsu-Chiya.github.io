---
title: Project Euler 366
tags:
  - 博弈
category:
  - Project Euler
mathjax: true
date: 2022-08-21 23:50:57
---

<escape><!-- more --></escape>

# Project Euler 366

## 题目

### Stone Game III

Two players, Anton and Bernhard, are playing the following game.

There is one pile of $n$ stones.

The first player may remove any positive number of stones, but not the whole pile.

Thereafter, each player may remove at most twice the number of stones his opponent took on the previous move.

The player who removes the last stone wins.

E.g. $n=5$

If the first player takes anything more than one stone the next player will be able to take all remaining stones.

If the first player takes one stone, leaving four, his opponent will take also one stone, leaving three stones.

The first player cannot take all three because he may take at most $2\times1=2$ stones. So let's say he takes also one stone, leaving $2$. The second player can take the two remaining stones and wins.

So $5$ is a losing position for the first player.

For some winning positions there is more than one possible move for the first player.

E.g. when $n=17$ the first player can remove one or four stones.

Let $M(n)$ be the maximum number of stones the first player can take from a winning position *at his first turn* and $M(n)=0$ for any other position.

$\sum M(n)$ for $n\le100$ is $728$.

Find $\sum M(n)$ for $n\le10^{18}$. Give your answer modulo $10^8$.

## 解决方案

通过以下程序，直接打印出$M$的前$1000$项的值：

```C++
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N=1000;
bool f[N+4][N+4],v[N+4][N+4];
bool ok(int n,int m){
    if(n==0) return 0;
    else if(n<=m) return 1;
    else if(v[n][m]) return f[n][m];
    v[n][m]=1;
    bool flag=0;
    for(int i=1;i<=m&&!flag;i++)
        if(!ok(n-i,i*2)) flag=1;
    return f[n][m]=flag;
}
int main(){
    for(int n=1;n<=N;n++){
        int ans=0;
        for(int i=1;i<n;i++){
            if(!ok(n-i,i*2)) ans=i;
        }
        printf("%d %d\n",n,ans);
    }
}
```

假设第$i$个斐波那契数的值为$f_i$，其中$f_1=1,f_2=2$。发现对于区间$[f_i,f_{i+1})$内的任意整数，函数值$M$是由一些连续的相邻整数段组成。更具体的解释为：

- 如果$x\le \left\lfloor\dfrac{f_i-1}{2}\right\rfloor$，有$M(f_i+x)=x;$
- 否则，对于$\left\lfloor\dfrac{f_i-1}{2}\right\rfloor< x< f_{i-1}$，有$M(f_i+x)=M(x).$

令$S(n)=\sum_{i=1}^n M(i)$，那么我们直接进行分段计算。对于区间$[f_i,f_{i+1})$的值，令$m_i=\left\lfloor\dfrac{f_i-1}{2}\right\rfloor$，那么有$S(f_{i+1}-1)-S(f_i-1)=\dfrac{m_i(m_i+1)}{2}+S(f_{i-1}-1)-S(m_i)$。

暴力分块计算即可，另外使用记忆化搜索进行加速。

## 代码

```py
N = 10 ** 18
mod = 10 ** 8
mp = {0: 0, 1: 0, 2: 0}


def S(n):
    if n in mp.keys():
        return mp[n]
    a, b, c = 1, 1, 2
    s = 0
    while True:
        if c > n:
            c = n + 1
        m = (b - 1) >> 1
        if b + m <= n:
            s += m * (m + 1) // 2 + S(a - 1) - S(m)
        else:
            k = n - b
            s += k * (k + 1) // 2
        if c == n + 1:
            break
        a, b, c = b, c, b + c
    mp[n] = s
    return s


ans = S(N) % mod
print(ans)

```
