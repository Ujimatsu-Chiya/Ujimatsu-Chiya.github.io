---
title: Project Euler 313
category:
  - Project Euler
tags:
mathjax: true
date: 2022-07-08 17:06:20
---

<escape><!-- more --></escape>

# Project Euler 313

## 题目

### Sliding game

In a sliding game a counter may slide horizontally or vertically into an empty space. The objective of the game is to move the red counter from the top left corner of a grid to the bottom right corner; the space always starts in the bottom right corner. For example, the following sequence of pictures show how the game can be completed in five moves on a $2$ by $2$ grid.

![](../images/p313_sliding_game_1.gif)

Let $S(m,n)$ represent the minimum number of moves to complete the game on an $m$ by $n$ grid. For example, it can be verified that $S(5,4) = 25$.

![](../images/p313_sliding_game_2.gif)

There are exactly $5482$ grids for which $S(m,n) = p^2$, where $p < 100$ is prime.

How many grids does $S(m,n) = p^2$, where $p < 10^6$ is prime?

## 解决方案

以一个比较低效的广度优先搜索打印出一部分$S(n,m)(n,m\ge2)$的值：

```py
N = 15


def solve(n, m):
    from queue import Queue
    dx, dy = [-1, 1, 0, 0], [0, 0, -1, 1]
    st = 1, 1, n, m
    mp = {st: 0}
    q = Queue()
    q.put(st)
    while q.qsize() > 0:
        rx, ry, ex, ey = q.get()
        if rx == n and ry == m:
            return mp[rx, ry, ex, ey]
        for i in range(4):
            fx, fy = ex + dx[i], ey + dy[i]
            if rx == fx and ry == fy:
                sx, sy = ex, ey
            else:
                sx, sy = rx, ry
            if 1 <= fx <= n and 1 <= fy <= m and (sx, sy, fx, fy) not in mp.keys():
                mp[sx, sy, fx, fy] = mp[rx, ry, ex, ey] + 1
                q.put((sx, sy, fx, fy))


for n in range(2, N):
    for m in range(2, N):
        print(solve(n, m), end=' ')
    print()

```

可以发现以下规律：

$$
s(m,n)=
\left \{\begin{aligned}
  &6m+2n-13  & & \text{if\quad} m>n \\
  &8m-11 & & \text{else if\quad} m=n \\
  &s(n,m) & & \text{else}
\end{aligned}\right.
$$

不难证明，不存在一个平方数，其模$8$的值为$5$，因此不考虑$s(m,m)$的情况。

对于每一个质数$p$，现在的问题就是求有多少$m$满足以下条件：

1. $n=\dfrac{p^2+13-6m}{2}$
2. $1<n$
3. $n<m$

联立第一个和第二个，得到$m<\dfrac{p^2+11}{6}$。联立第一个和第三个，得到$m>\dfrac{p^2+13}{8}$。最终就是求区间$\left(\dfrac{p^2+13}{8},\dfrac{p^2+11}{6}\right)$的整数个数。

枚举所有质数$p$将这些区间中的整数个数相加即可。

## 代码

```C++
# include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N=1000000;
vector<int>pr;
bool b[N+4];
int main(){
    for(int i=2;i<N;i++){
        if(b[i]) continue;
        pr.push_back(i);
        for(ll j=1ll*i*i;j<N;j+=i)
            b[j]=1;
    }
    ll ans=0;
    for(int p:pr)
        ans+=(1ll*p*p+11+5)/6-1-(1ll*p*p+13)/8;
    ans<<=1;
    printf("%lld\n",ans);
}

```
