---
title: Project Euler 706
tags:
  - Project Euler
  - 动态规划
mathjax: true
---
<escape><!-- more --></escape>

# Project Euler 706

## 题目

### 3-Like Numbers

For a positive integer $n$, define $f(n)$ to be the number of non-empty substrings of $n$ that are divisible by $3$. For example, the string "$2573$" has $10$ non-empty substrings, three of which represent numbers that are divisible by $3$, namely $57, 573$ and $3$. So $f(2573) = 3$.

If $f(n)$ is divisible by $3$ then we say that $n$ is *$3$-like*.

Define $F(d)$ to be how many $d$ digit numbers are $3$-like. For example, $F(2) = 30$ and $F(6) = 290898$.

Find $F(10^5)$. Give your answer modulo $1\,000\,000\,007$.

## 解决方案

一个非常直接的动态规划题。

令$N=10^5.$考虑到子串的个数，通常我们先将这个数$d=d_1d_2d_3\dots$看成一个字符串，然后令其前缀和数组为$s$，其中$s[0]=0,s[i]=s[i-1]+d_i$，那么一个数的子串和就可以通过数组$s$进行一次减法求得。

令$N=10^5$，假设已有状态$f(i,c_1,c_2,k,t)(1\le i\le N,0\le c_1,c_2,t<3)$为有多少个$i$位数满足以下条件：

- 令$c_0=(i+1-c_1-c_2)\%3$。这两个值其实也是状态之一，只不过可以被$i,c_1,c_2$表出。
- 目前数组$s$一共有$i+1$项，其中有$c_j$个项模$3$的值为$j(0\le j<3)$ ，注意$c_j$已经被$3$取模。
- 目前$s[i]$的值为$k$。
- 子串个数和$t$关于模$3$同余。

那么状态的转移只需要考虑在每个数后面添加一个数位$0\sim 9$，注意维护前缀和数组$s$新的一项。

本题转移过程考虑进行我为人人式。

不难知道初值$f(1,0,0,0,1)=f(1,1,0,1,0)=f(1,0,1,2,0)=3$，这$3$种情况分别对应一位数模$3$余$0$，模$3$余$1$，模$3$余$2$的情况。

以$k=0$为例，那么有三种方式转移：

$\begin{aligned}
& f(i,c_1,c_2,0,t)\cdot 4\rightarrow f(i+1,c_1,c_2,0,(t+c_0)\%3) \\
& f(i,c_1,c_2,0,t)\cdot 3\rightarrow f(i+1,(c_1+1)\%3,c_2,1,(t+c_1)\%3) \\
& f(i,c_1,c_2,0,t)\cdot 3\rightarrow f(i+1,c_1,(c_2+1)\%3,1,(t+c_2)\%3) \\
\end{aligned}$

由于目前的前缀和$s[i]=0$，那么再添加数位$0,3,6,9$中的一个，那么$s[i+1]=0$，因此这时就多了$c_0$个符合题意的子串；如果添加数位$1,4,7$中的一个，那么$s[i+1]=1$，因此这时就多了$c_1$个符合题意的子串；如果添加一个数位$2,5,8$，那么$s[i+1]=2$，因此这时就多了$c_2$个符合题意的子串。

因此，最终答案为

$$\sum_{c_1=0}^3\sum_{c_2=0}^3\sum_{k=0}^3f(N,c_0,c_1,k,0)$$

本题也可以将整个状态转移过程写成一个$81\times81$大小的矩阵，通过矩阵快速幂以$O(\log N)$直接计算出结果。此处不再详述这个优化。

## 代码

```C++
# include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N=100000;
ll f[N+4][3][3][3][3],mod=1e9+7;
void add(ll &x,ll y){
    x=(x+y)%mod;
}
int main() {
    f[1][0][0][0][1] = 3;
    f[1][1][0][1][0] = 3;
    f[1][0][1][2][0] = 3;
    for (int i = 1; i < N; i++)
        for (int c1 = 0; c1 < 3; c1++)
            for (int c2 = 0; c2 < 3; c2++)
                for (int t = 0; t < 3; t++) {
                    int c0 = (i + 1 - c1 - c2 + 6) % 3;
                    ll &now0 = f[i][c1][c2][0][t], &now1 = f[i][c1][c2][1][t], &now2 = f[i][c1][c2][2][t];
                    add(f[i + 1][c1][c2][0][(t + c0) % 3], now0 * 4); //0,3,6,9
                    add(f[i + 1][(c1 + 1) % 3][c2][1][(t + c1) % 3], now0 * 3);//1,4,7
                    add(f[i + 1][c1][(c2 + 1) % 3][2][(t + c2) % 3], now0 * 3);//2,5,8

                    add(f[i + 1][(c1 + 1) % 3][c2][1][(t + c1) % 3], now1 * 4);//0,3,6,9
                    add(f[i + 1][c1][(c2 + 1) % 3][2][(t + c2) % 3], now1 * 3);// 1,4,7
                    add(f[i + 1][c1][c2][0][(t + c0) % 3], now1 * 3);//2,5,8

                    add(f[i + 1][c1][(c2 + 1) % 3][2][(t + c2) % 3], now2 * 4);//0,3,6,9
                    add(f[i + 1][c1][c2][0][(t + c0) % 3], now2 * 3);//1,4,7
                    add(f[i + 1][(c1 + 1) % 3][c2][1][(t + c1) % 3], now2 * 3);//2,5,8
                }
    ll ans = 0;
    for (int c1 = 0; c1 < 3; c1++)
        for (int c2 = 0; c2 < 3; c2++)
            for (int k = 0; k < 3; k++)
                add(ans, f[N][c1][c2][k][0]);
    printf("%lld\n", ans);
}

```
