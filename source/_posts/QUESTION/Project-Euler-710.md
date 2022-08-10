---
title: Project Euler 710
category:
  - Project Euler
tags:
  - 动态规划
mathjax: true
date: 2022-07-17 23:11:44
---

<escape><!-- more --></escape>

# Project Euler 710

## 题目

### One Million Members

**On Sunday 5 April 2020 the Project Euler membership first exceeded one million members. We would like to present this problem to celebrate that milestone. Thank you to everyone for being a part of Project Euler.**

The number $6$ can be written as a palindromic sum in exactly eight different ways:

$$(1, 1, 1, 1, 1, 1), (1, 1, 2, 1, 1), (1, 2, 2, 1), (1, 4, 1), (2, 1, 1, 2), (2, 2, 2), (3, 3), (6)$$

We shall define a *twopal* to be a palindromic tuple having at least one element with a value of $2$. It should also be noted that elements are not restricted to single digits. For example, $(3, 2, 13, 6, 13, 2, 3)$ is a valid twopal.

If we let $t(n)$ be the number of twopals whose elements sum to $n$, then it can be seen that $t(6) = 4$:

$$(1, 1, 2, 1, 1), (1, 2, 2, 1), (2, 1, 1, 2), (2, 2, 2)$$

Similarly, $t(20) = 824$.

In searching for the answer to the ultimate question of life, the universe, and everything, it can be verified that $t(42) = 1999923$, which happens to be the first value of $t(n)$ that exceeds one million.

However, your challenge to the "ultimatest" question of life, the universe, and everything is to find the least value of $n \gt 42$ such that $t(n)$ is divisible by one million.

## 解决方案

不难想到使用动态规划解决本题。

由于回文序列的左右两半是完全相同的，因此只考虑其中的一半。

令状态$f_0(i)(i\ge 0)$表示当前序列**不存在**$2$的情况下，能够组成和为$i$的任意长度序列有多少个，那么不难写出状态转移方程为：

$$
f_0(i)=
\left \{\begin{aligned}
  &1 & & \text{if}\quad  i\le1 \\
  &\sum_{j=1}^{i} f_0(i-j)-f_0(i-2)& & \text{else}
\end{aligned}\right.
$$

上面的方程表示将状态$f_0(i-j)$中的所有序列都添加一个$i$，那么就成为了$f_0(i)$中的序列，当然$j$不能为$2$，因此后面减去$f_0(i-2)$。

令$f_1(i)(i\ge 0)$表示当前序列**存在**$2$的情况下，能够组成和为$i$的任意长度序列有多少个，那么不难写出状态转移方程为：

$$
f_1(i)=
\left \{\begin{aligned}
  &0 & & \text{if}\quad  i\le1 \\
  &\sum_{j=1}^{i} f_1(i-j)+f_0(i-2)& & \text{else}
\end{aligned}\right.
$$

上面的方程表示将状态$f_1(i-j)$中的所有序列都添加一个$i$，那么就成为了$f_1(i)$中的序列；此外，将$f_0(i-2)$中的序列再添加一个$2$，那么这个序列就存在了$2$，变成了状态$f_1(i)$.

回到本题，如果需要求$t(N)$，那么

- 当$N$为奇数时，这个回文序列必定为奇数长度，并且中间的数必为奇数，所以两边的数必定有$2$。因此$t(N)=\sum_{i=1}^{\frac{N-1}{2}}f_1(i).$
- 当$N$为偶数时，考虑严格在序列两边的数，这些数必定存在一个为$2$（这种情况和奇数时一样）；如果没有$2$，那么序列的长度必定为奇数长度，并且中间的值为$2$。因此$t(N)=\sum_{i=1}^{\frac{N}{2}}f_1(i)+f_0\left(\dfrac{N}{2}-1\right).$

最终从小到大枚举$N$即可。

## 代码

```C++
# include <bits/stdc++.h>
using namespace std;
const int N = 2000004;
int s[N][2],f[N][2],mod=1000000;
int main(){
    f[0][0]=s[0][0]=1;
    f[1][0]=1;s[1][0]=2;
    int ans=0;
    for(int n=2;n<N;n++){
        f[n][0]=(s[n-1][0]-f[n-2][0]+mod)%mod;
        f[n][1]=(s[n-1][1]+f[n-2][0])%mod;
        s[n][0]=(s[n-1][0]+f[n][0])%mod;
        s[n][1]=(s[n-1][1]+f[n][1])%mod;
        int a=s[n/2][1];
        if(n%2==0) a=(a+f[n/2-1][0])%mod;
        if(n>42&&a%mod==0) {ans=n;break;}
    }
    printf("%d\n",ans);
}
```
