---
title: Project Euler 256
category:
  - Project Euler
tags:
  - 论文
mathjax: true
date: 2022-08-05 21:40:20
---

<escape><!-- more --></escape>

# Project Euler 256

## 题目

### Tatami-Free Rooms

Tatami are rectangular mats, used to completely cover the floor of a room, without overlap.

Assuming that the only type of available tatami has dimensions $1\times2$, there are obviously some limitations for the shape and size of the rooms that can be covered.

For this problem, we consider only rectangular rooms with integer dimensions $a, b$ and even size $s = a\cdot b$.

We use the term 'size' to denote the floor surface area of the room, and — without loss of generality — we add the condition $a\le b$.

There is one rule to follow when laying out tatami: there must be no points where corners of four different mats meet.

For example, consider the two arrangements below for a $4\times4$ room:

![](../images/p256_tatami3.gif)

The arrangement on the left is acceptable, whereas the one on the right is not: a red "<font color="#FF0000">**X**</font>" in the middle, marks the point where four tatami meet.

Because of this rule, certain even-sized rooms cannot be covered with tatami: we call them tatami-free rooms.

Further, we define $T(s)$ as the number of tatami-free rooms of size $s$.

The smallest tatami-free room has size $s = 70$ and dimensions $7\times10$.

All the other rooms of size $s = 70$ can be covered with tatami; they are: $1\times70, 2\times35$ and $5\times14$.

Hence, $T(70) = 1$.

Similarly, we can verify that $T(1320) = 5$ because there are exactly $5$ tatami-free rooms of size $s = 1320$:

$20\times66, 22\times60, 24\times55, 30\times44$ and $33\times40$.

In fact, $s = 1320$ is the smallest room-size $s$ for which $T(s) = 5$.

Find the smallest room-size $s$ for which $T(s) = 200$.

## 解决方案

本解决方案参考了Thread中的一些内容。

这篇[论文](http://webhome.cs.uvic.ca/~ruskey/Publications/Tatami/TatamiDraftSubmitted.pdf)给出了关于每一种房间$a\times b$铺满榻榻米的方案数$T(a,b)$。

分开两种情况讨论：$a$为奇数和$a$为偶数的情况。

当$a$是奇数时，定理$2.3$指出，$a\times b$的铺设方案将会由$a\times(a-1)$和$a\times(a+1)$的铺设方案组合而成。

因此，如果$T(a,b)>0$，那么$b$是偶数，并且存在一个$k>0$使得：$k(a-1)\le b\le k(a+1)$。换言之，如果$T(a,b)=0$，那么存在一个$k>0$使得$(a+1)\cdot k+2\le b\le(a-1)\cdot(k+1)-2$，恰好是上面区间的补。

当$a$为偶数时，定理$2.4$指出，$a\times b$的铺设方案将会由$a\times a,a\times (a-2),a\times 1$的铺设方案组合而成。其中，$a\times1$的铺设方案会出现在$a\times (a-2),a\times a$这两种铺设方案的任意两个之间。并且，$a\times1$这种铺设方案还可以出现在第$1$列或者第$n$列，也可以不出现。

如果$a\times(a-2)$和$a\times a$的铺设方案总共有$k$块，那么$a\times 1$的铺设方案块数在$k-1\sim k+1$之间。因此，如果$T(a,b)>0$，那么存在$k$，使得$k(a-2)+k-1\le b\le ka+k+1$；那么和奇数的情况类似，如果$T(a,b)=0$，那么存在一个$k>0$使得$(a+1)\cdot k+2\le b\le(a-1)\cdot(k+1)-2$。

最终发现，两种情况的结论是一样的，即一个$a\times b$的偶数面积矩形是无法铺满榻榻米的房间当且仅当存在一个整数$k$，满足：

$$(a+1)\cdot k+2\le b\le(a-1)\cdot(k+1)-2$$

因此，第一重循环枚举$a$，二重枚举$k$，最终枚举这个区间内的$b$值即可。

本题上限难以确定，此处假设为$N=10^8$。

## 代码

```C++
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const int Q=200;
const ll N=100000000ll;
int cnt[N+4];
int solve(){
    for(ll a=1;a*a<=N;a++){
        for(ll k=1;(a+1)*k+2<=(a-1)*(k+1)-2&&a*((a+1)*k+2)<=N;k++){
            for(ll b=(a+1)*k+2;b<=(a-1)*(k+1)-2&&a*b<=N;b++){
                if(a&b&1) continue;
                ++cnt[a*b];
            }
        }
    }
    for(int i=0;i<=N;i+=2)
        if(cnt[i]==Q) return i;
}
int main(){
    int ans = solve();
    printf("%d\n",ans);
}

```
