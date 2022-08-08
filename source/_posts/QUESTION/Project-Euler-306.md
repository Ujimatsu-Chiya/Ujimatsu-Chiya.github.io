---
title: Project Euler 306
category:
  - Project Euler
tags:
  - 博弈论
  - SG定理
mathjax: true
date: 2022-07-06 13:08:45
---

<escape><!-- more --></escape>

# Project Euler 306

## 题目

### Paper-strip Game

The following game is a classic example of Combinatorial Game Theory:

Two players start with a strip of $n$ white squares and they take alternate turns.

On each turn, a player picks two contiguous white squares and paints them black.

The first player who cannot make a move loses.

- $n = 1$: No valid moves, so the first player loses automatically.
- $n = 2$: Only one valid move, after which the second player loses.
- $n = 3$: Two valid moves, but both leave a situation where the second player loses.
- $n = 4$: Three valid moves for the first player, who is able to win the game by painting the two middle squares.
- $n = 5$: Four valid moves for the first player (shown below in red), but no matter what the player does, the second player (blue) wins.

![](../images/p306_pstrip.gif)

So, for $1 \le n \le 5$, there are $3$ values of $n$ for which the first player can force a win.

Similarly, for $1 \le n \le 50$, there are 40 values of $n$ for which the first player can force a win.

For $1 \le n \le 1 000 000$, how many values of $n$ are there for which the first player can force a win?

## Sprague–Grundy定理

$sg$函数是一个用来解决公平组合游戏(ICG)问题的一种工具。

定义一个非负整数集合上的运算$\text{mex}(s)$：表示集合$s$中未出现的最小的非负整数。

我们定义一个游戏状态$n$，令$sg(n)=\text{mex}(\{sg(m)|n\rightarrow m\})$.$m$是从$n$能够抵达的所有游戏状态。如果$sg(n)>0$，那么状态$n$为必胜态；如果$sg(n)=0$，那么为必败态。

[Sprague–Grundy，SG定理](https://en.wikipedia.org/wiki/Sprague%E2%80%93Grundy_theorem)说明了，如果这个游戏当前的状态$n$，它可以看做是多个状态$(n_1,n_2,\dots,n_k)$的组合，那么就可以写成：

$$sg(n)=sg(n_1)\oplus sg(n_2)\oplus \dots \oplus sg(n_k)$$

以NIM游戏为例，如果当前有$n$堆石头，其中第$i$堆为$a_i$。那么状态$sg(a_1,a_2,\dots,a_n)$可以看成是$sg(a_1),sg(a_2),\dots,sg(a_n)$的组合，当前的状态是必胜态还是必败态由$sg(a_1)\oplus sg(a_2)\oplus\dots\oplus sg(a_n)$决定。

因此一般使用SG定理解决问题，主要依靠的是分治的思想。

## 解决方案

当双方每一次占用相邻的格子时，可以把它看成是将一个长度为$n$的纸条，将其中相邻的两格占用后，产生了两个长度分别为$i,n-2-i(0\le i\le n-2-i)$的纸条。

因此我们可以将一个长度为$n$的纸条看做是一个状态，设其为$sg(n)(n\ge 0)$.那么$sg(n)$的值就可以通过以下值计算出：

$$
sg(n)=
\left \{\begin{aligned}
  &0 & & \mathrm{if\quad} n\le 1 \\
  &\text{mex}(\{sg(i)\oplus sg(n-2-i)|0\le i\le n-2-i\}) & & \mathrm{else}
\end{aligned}\right.
$$

使用如下代码打印出这个游戏的$sg$函数前一部分序列，在OEIS中查询到结果为[A002187](http://oeis.org/A002187)。

```C++
# include <bits/stdc++.h>
using namespace std;
typedef unsigned long long ull;
const int N=100;
int sg[N+4];
bool mex[N+4];
int main(){
    for(int i=1;i<=N;i++){
        memset(mex,0,sizeof(mex));
        int j=0;
        for(j=0;j<=i-j-2;j++)
            mex[sg[j]^sg[i-j-2]]=1;
        for(j=0;mex[j];++j);
        sg[i]=j;
    }
    for(int i=0;i<=N;i++)
        printf("%d ",sg[i]);
}

```

在FORMULA一栏中查找到这个信息：

``` 
Has period 34 with the only exceptions at n=0, 14, 16, 17, 31, 34 and 51.
```

这说明这个$sg$函数是一个以$34$为周期的序列，除了$0,14,16,17,31,34,51$这几个状态。

因此，计算时只需要单独考虑$1\sim 51$这几个项即可。

## 代码

```py
N = 10 ** 6
a = [0, 1, 1, 2, 0, 3, 1, 1, 0, 3, 3, 2, 2, 4, 0, 5, 2, 2, 3, 3, 0, 1, 1, 3, 0, 2, 1, 1, 0, 4, 5, 2, 7, 4, 0, 1, 1, 2,
     0, 3, 1, 1, 0, 3, 3, 2, 2, 4, 4, 5, 5, 2]
t = [3, 3, 0, 1, 1, 3, 0, 2, 1, 1, 0, 4, 5, 3, 7, 4, 8, 1, 1, 2, 0, 3, 1, 1, 0, 3, 3, 2, 2, 4, 4, 5, 5, 9]
ans = sum(a[i] > 0 for i in range(min(N, len(a))))
if N > len(a):
    N -= len(a)
    block, res = divmod(N, len(t))
    ans += block * (len(t) - t.count(0)) + res - t[:res].count(0)
print(ans)

```
