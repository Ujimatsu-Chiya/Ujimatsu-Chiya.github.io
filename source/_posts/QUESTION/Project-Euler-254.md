---
title: Project Euler 254
tags:
  - Project Euler
  - 贪心
mathjax: true
date: 2022-07-04 18:02:50
---

<escape><!-- more --></escape>

# Project Euler 254

## 题目

### Sums of Digit Factorials

Define $f(n)$ as the sum of the factorials of the digits of $n$. For example, $f(342) = 3! + 4! + 2! = 32$.

Define $sf(n)$ as the sum of the digits of $f(n)$. So $sf(342) = 3 + 2 = 5$.

Define $g(i)$ to be the smallest positive integer $n$ such that $sf(n) = i$. Though $sf(342)$ is $5$, $sf(25)$ is also $5$, and it can be verified that $g(5)$ is $25$.

Define $sg(i)$ as the sum of the digits of $g(i)$. So $sg(5) = 2 + 5 = 7$.

Further, it can be verified that $g(20)$ is $267$ and $\sum sg(i)$ for $1 \le i \le 20$ is $156$.

What is $\sum sg(i)$ for $1 \le i \le 150$?

## 解决方案

本解决方案参考了Thread中的一些内容。

注意到一个特点：函数$f,sf$的计算过程中，只和每个数位本身的值有关，和数位在哪个位置无关。因此，$g(i)$的值一定是一个如此的数：在**长度最短的基础**上，从高位到低位是非递减的。

这道题目使用了两次贪心思想：

1. <u>为了求$g(i)$时的值$n$最小，那么$f(n)$这个值也应该最小</u>，此时$f(n)$的值**至多**以一个非$9$的数开头，然后都以$9$为结尾（如$19,299,9999$等）。
2. 根据上述特点，确定好$f(n)$后，划分$f(n)$的值时，先尽量取完$9$，再尽量取$8$，……，一直到尽量取完$1$。我们用一个向量$\vec{a}=(a_1,a_2,\dots,a_8,a_9)$来表示这时的取数情况，并且$g(i)$应该是由$a_1$个$1$，$a_2$个$2$，……，$a_9$个$9$拼接起来成的一个数。此后我们讨论$g(i)$时，$g(i)$就用这种向量来表示。

但是，这种贪心思想在求$g(i)$，$i$比较大时是有效的，但是在$i$比较小时，上述第一次的贪心思想不成立（举个例子，$f(59)=363000,f(65)=840,sf(59)=sf(65)=12$）。因此为了规避，考虑小范围内（$63$以下）暴力枚举$f(n)$的值，大范围内（$63$及以上）贪心构造$f(n)$的值。

令$s(\vec{a})=\sum_{k=1}^9 a_k,ds(\vec{a})=\sum_{k=1}^9 k\cdot a_k$.如果一个向量$\vec{a}$比向量$\vec{b}$更优，那么$s(\vec{a})<s(\vec{b})$，或者是$s(\vec{a})=s(\vec{b})$并且$\vec{a}$的“字典序”要**大于**$\vec{b}$。

令$h(i)=(a_1^i,a_2^i,\dots,a_9^i)$是将数$i$按照上面第二次贪心思想进行划分的结果，用上面定义的向量表示；令$t(n)$表示$n$的各位数字之和。对于所有$1\le i\le 9!$，先用贪心的思想预处理出$h(i)$（注意这时所有的$a_9^i=0$）。接下来暴力**枚举**小范围的$f(n)$值（这里是枚举$10^7$以下的所有$f(n)$），那么$g(t(f(n)))$的一个候选值就是$h(f(n))$，最终将这些小范围的$g(i)$中最优的向量求出来。

在大范围内，给定一个$i$，我们就可以按照贪心思想确定对应的$f(n)$值，这个值是$(i\%9+1)\cdot 10^{\lfloor\frac{i}{9}\rfloor}-1$。确定了$f(n)$后，就可以按照第一次贪心的思想直接构造出$g(i)$最优的向量。

最终，将所有最优的向量的$ds$函数值计算并相加即可。

## 代码

```C++
# include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const int Q=150;
const int S=9,W=362880,N=63,B=19,MX=1e7;
ll pw[B],fac[B];
int h[W][S],ds[W],s[W];
int sq[N],pq[N][S];
// 如果b字典序更大，b更优。
bool ok(int a[],int b[]) {
    for (int i = 0; i < S; i++)
        if (a[i] != b[i]) return a[i] < b[i];
    return false;
}
int main() {
    pw[0] = fac[0] = 1;
    for (int i = 1; i < B; i++)
        pw[i] = pw[i - 1] * 10, fac[i] = fac[i - 1] * i;
    // 每个数i，贪心取最大的值，尽量取完，然后再取最小的。h[i][j]表示从i中分出h[i][j]个fac[j]。
    for (int i = 0; i < W; i++) {
        for (int j = 8, t = i; j > 0; j--) {
            h[i][j] = t / fac[j];
            ds[i] += h[i][j] * j;
            s[i] += h[i][j];
            t %= fac[j];
        }
    }
    //1~62时直接暴力枚举。枚举范围是10^7。
    for (int fn = 0; fn <= MX; fn++) {
        int a = fn / W, b = fn % W;
        int sum = 0;
        for (int x = fn; x; x /= 10)
            sum += x % 10;
        if (sum >= N) continue;
        //sq[n]：目前最优的g(fn的数位之和)中的数位个数。pq[n]：目前最优的g(fn的数位之和)中的向量。
        if (sq[sum] == 0 || sq[sum] > s[b] + a || sq[sum] == s[b] + a && ok(pq[sum], h[b])) {
            sq[sum] = s[b] + a;
            for (int i = 0; i < S; i++)
                pq[sum][i] = h[b][i];

        }
    }
    ll ans = 0;
    for (int i = 1; i <= Q && i < N; i++) {
        ans += sq[i] * 9;
        for (int j = 1; j < S; j++)
            ans -= pq[i][j] * (9 - j);
    }
    //63以后全部贪心取9。
    for (int i = N; i <= Q; i++) {
        ll t = (i % 9 + 1) * pw[i / 9] - 1;
        printf("%lld\n",t);
        ans += (t / W) * 9 + ds[t % W];
    }
    printf("%lld\n", ans);
}

```
