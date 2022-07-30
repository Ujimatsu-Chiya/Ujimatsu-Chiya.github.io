---
title: Project Euler 649
tags:
  - Project Euler
  - SG定理
  - 动态规划
  - 矩阵快速幂&#43;
mathjax: true
date: 2022-07-27 23:49:29
---

<escape><!-- more --></escape>

# Project Euler 649

## 题目

### Low-Prime Chessboard Nim

Alice and Bob are taking turns playing a game consisting of $c$ different coins on a chessboard of size $n$ by $n$.

The game may start with any arrangement of $c$ coins in squares on the board. It is possible at any time for more than one coin to occupy the same square on the board at the same time. The coins are distinguishable, so swapping two coins gives a different arrangement if (and only if) they are on different squares.

On a given turn, the player must choose a coin and move it either left or up $2$, $3$, $5$, or $7$ spaces in a single direction. The only restriction is that the coin cannot move off the edge of the board.

The game ends when a player is unable to make a valid move, thereby granting the other player the victory.

Assuming that Alice goes first and that both players are playing optimally, let $M(n, c)$ be the number of possible starting arrangements for which Alice can ensure her victory, given a board of size $n$ by $n$ with $c$ distinct coins.

For example, $M(3, 1) = 4$, $M(3, 2) = 40$, and $M(9, 3) = 450304$.

What are the last $9$ digits of $M(10\,000\,019, 100)$?

## 解决方案

令$N=10000019,C=100$。注意到，游戏中硬币之间是独立的，没有任何关系，因此多个硬币的游戏局面考虑用SG定理组合出来。

考虑单独一个硬币时的局面。一个硬币可以向左或向上移动，并且一次只能朝其中一个方向移动$2,3,5,7$格。那么棋盘的两个方向也是相互独立的，同样也可以通过SG定理组合出来。

两个坐标之间是独立的，硬币之间也是独立的，因此我们可以将这个游戏可以看成是$2C$个局面的组合。

那么考虑一个硬币时一维的情况（也就是单独一个局面时的情况）。假设当前硬币在第$n$格，那么它就只能移向第$n-2,n-3,n-5,n-7$格。因此$n$的SG函数值不难写出为：

$$
sg(n)=
\left \{\begin{aligned}
  &0 & & \mathrm{if\quad} n\le 2 \\
  &\text{mex}(\{sg(n-x)|x\in\{2,3,5,7\}\wedge x<n\}) & & \mathrm{else}
\end{aligned}\right.
$$

其中运算$\text{mex}(s)$表示集合$s$中未出现的最小的非负整数。那么使用一下程序直接进行打表：

```C++
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N=40,M=500;
int sg[N+4],c[8];
bool mex[144];
vector<int>z{2,3,5,7};
int main(){
    for(int i=1;i<=N;i++){
        memset(mex,0,sizeof(mex));
        for(int x:z)
            if(i-x>0) mex[sg[i-x]]=1;
        int j=0;
        for(;mex[j];++j);
        sg[i]=j;
        printf("%d\n",j);
    }
}



```

打完表后发现，从$1$开始，$sg$函数值是一个周期为$9$的序列，其中一个周期的序列为$[0,0,1,1,2,2,3,3,4]$。

因此，用一个数组$c[i]$表示$1\sim N$中有多少个数的$sg$函数值为$i$。$c[i]$将会被很快地计算出。

最终问题转化为有多少种方法可以将$sg$函数值填入一个长度为$2C$的序列，并且这$2C$个值的异或和不为$0$。

令状态$f(i,j)(0\le i\le 2C,0\le j<2^3)$表示填入长度为$i$的序列，并且异或和为$j$的方案数有多少个。那么不难写出状态转移方程为：

$$
g(i,j)=
\left \{\begin{aligned}
  &1  & & \mathrm{if\quad} i=0\wedge j=0 \\
  &0 & & \mathrm{else if\quad} i=0 \\
  &\sum_{k=0}^{2^3-1} g(i-1,j\oplus k) \cdot c[k] & & \mathrm{else}
\end{aligned}\right.
$$

如果我们已经求出了长度为$a$的序列的各种填法$f(a,\cdot)$和长度为$b$的各种填法$f(b,\cdot)$，不难知道我们可以通过卷积组合出$f(a+b,\cdot)$。

枚举所有的$f(a,i)$和$f(b,j)$，将这两部分值直接合并起来：

$f(a,i)\cdot f(b,j)\rightarrow f(a+b,i\oplus j)$

因此，这给了我们一个方案：依次求出$f(2^0,\cdot),f(2^1,\cdot),f(2^2,\cdot),\dots$。然后针对$N$，选择这些求出的$f(2^i,\cdot,\cdot)$进行合并即可。

最终答案为$\sum_{i=1}^{2^3-1} f(N,i)$。

## 代码

```C++
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N=10000019;
const int C=100;
const int D=1<<3;
ll mod=1000000000;
int sg[10]={0,0,0,1,1,2,2,3,3,4};
ll a[D],b[D];
void cal(ll a[D],ll b[D],ll ans[D]){
    ll c[D]={0};
    for(int i=0;i<D;i++)
        for(int j=0;j<D;j++)
            c[i^j]=(c[i^j]+a[i]*b[j])%mod;
    memcpy(ans,c,sizeof(c));
}
int main(){
    for(int i=1;i<=9;i++)
        b[sg[i]]+=(N+9-i)/9%mod;
    a[0]=1;
    for(int c=C*2;c;c>>=1){
        if(c&1) cal(a,b,a);
        cal(b,b,b);
    }
    ll ans=0;
    for(int i=1;i<D;i++)
        ans=(ans+a[i])%mod;
    printf("%lld\n",ans);
}

```
