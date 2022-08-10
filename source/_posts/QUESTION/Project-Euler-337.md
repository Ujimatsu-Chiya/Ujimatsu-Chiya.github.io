---
title: Project Euler 337
category:
  - Project Euler
tags:
  - 动态规划
  - 树状数组
mathjax: true
date: 2022-06-05 09:28:53
---

<escape><!-- more --></escape>

# Project Euler 337

## 题目

### Totient Stairstep Sequences

Let $\{a_1, a_2,\dots, a_n\}$ be an integer sequence of length n such that:

- $a_1 = 6$
- for all $1 \le i < n$ : $\varphi(a_i) < \varphi(a_{i+1}) < a_i < a_{i+1}\quad ^1$

Let $S(N)$ be the number of such sequences with $a_n \le N$.

For example, $S(10) = 4: \{6\}, \{6, 8\}, \{6, 8, 9\}$ and $\{6, 10\}$.

We can verify that $S(100) = 482073668$ and $S(10 000) \bmod 10^8 = 73808307$.

Find $S(20 000 000) \bmod 10^8$.

$^1 \quad \varphi$ denotes **Euler’s totient function**.

## 解决方案

在一个序列中，只有相邻的两个数才会有特定的放置关系，因此很容易想到动态规划的做法。

和往常一样，假设$f(i)(i\ge 6)$为以数$i$为**结尾**的序列的数量，那么我们可以得到以下状态转移方程：

$$
f(i)=
\left \{\begin{aligned}
  &1  & & \text{if}\quad i=6 \\
  &\sum_{j,\varphi(j)<\varphi(i)<j<i} f(j) & & \text{else}
\end{aligned}\right.
$$

不过，这种转移方式是$O(n^2)$的，如果为了使用树状数组优化，将转移过程下降到$O(n\log n)$，那么需要进行大量的预处理（因为根据上面的式子，$\varphi(a_{i+1})$的位置的难以确定）。

因此，使用另外一种转移方式。令$N=20000000$。假设$f(i)(6\le i\le N)$为以数$i$为**开头**的序列的数量，那么我们可以得到以下状态转移方程：

$$
f(i)=
\left \{\begin{aligned}
  &1  & & \text{if}\quad i=N \\
  &1+\sum_{j,\varphi(i)<\phi(j)<i<j} f(j) & & \text{else}
\end{aligned}\right.
$$

在计算$f(i)$时，树状数组已经保存了所有大于$i$时的状态值。因此，求出此时满足$\varphi(i)<\varphi(j)< i$的所有$j$，进行求和，而树状数组可以很方便地维护这一段的值之和。

在后面这个转移过程中，$f(6)$为最终答案。

## 代码

```C++
#include <bits/stdc++.h>
# define lb(x) ((x)&-(x))
using namespace std;
typedef long long ll;
const int N=20000000;
int phi[N+4];
int s[N+4],f[N+4],mod=1e8;
void add(int p,int x){
    for(int i=p;i<=N;i+=lb(i))
        s[i]=(s[i]+x)%mod;
}
int que(int p){
    int ans=0;
    for(int i=p;i;i-=lb(i))
        ans=(ans+s[i])%mod;
    return ans;
}
int main(){
    for(int i=1;i<=N;i++)
        phi[i]=i;
    for(int i=2;i<=N;i++){
        if(phi[i]==i){
            for(int j=i;j<=N;j+=i)
                phi[j]=phi[j]/i*(i-1);
        }
    }
    for(int i=N;i>=6;i--){
        int w=(que(i-1)-que(phi[i])+1+mod)%mod;
        add(phi[i],w);
        f[i]=w;
    }
    int ans=f[6];
    printf("%d\n",ans);
}

```
