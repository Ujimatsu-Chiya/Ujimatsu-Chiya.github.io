---
title: Project Euler 798
tags:
  - Project Euler
  - 快速沃尔什变换
  - SG定理
mathjax: true
date: 2022-08-05 21:41:05
---

<escape><!-- more --></escape>

# Project Euler 798

## 题目

### Card Stacking Game

Two players play a game with a deck of cards which contains $s$ suits with each suit containing $n$ cards numbered from $1$ to $n$.

Before the game starts, a set of cards (which may be empty) is picked from the deck and placed face-up on the table, with no overlap. These are called the visible cards.

The players then make moves in turn.

A move consists of choosing a card $X$ from the rest of the deck and placing it face-up on top of a visible card $Y$, subject to the following restrictions:

- $X$ and $Y$ must be the same suit;
- the value of $X$ must be larger than the value of $Y$.

The card $X$ then covers the card $Y$ and replaces $Y$ as a visible card.

The player unable to make a valid move loses and play stops.

Let $C(n, s)$ be the number of different initial sets of cards for which the first player will lose given best play for both players.

For example, $C(3, 2) = 26$ and $C(13, 4) \equiv 540318329 \pmod {1\,000\,000\,007}$.

Find $C(10^7, 10^7)$. Give your answer modulo $1\,000\,000\,007$.

## 解决方案

本解决方案参考了Thread中的内容，一开始我是直接暴力加FWT做出本题的。

令$N=M=10^7$。每一个花色可以看成是一个局面。整个游戏由多个不同花色组合而成，因此通过SG定理将最终游戏的SG函数值组合出来。由于$M$值过大，需要使用快速沃尔什变换解决异或卷积。

那么对于单个花色而言，一共有$N$张牌，因此**初始状态**一共有$2^N$种，每种初始状态对应一个$\{1,2,\dots,N\}$的子集。

枚举$2^N$个子集的$sg$函数值并统计个数。那么当$N=1,2,\dots,14$时，结果如下（从第$0$列起，第$j$列表示有多少个子集的$sg$函数值为$j$）：

```
   2
   3    1
   4    3    1
   6    6    3    1
  10   11    6    4    1
  18   20   11   10    4    1
  34   37   20   21   10    5    1
  66   70   37   41   21   15    5    1
 130  135   70   78   41   36   15    6    1
 258  264  135  148   78   77   36   21    6    1
 514  521  264  283  148  155   77   57   21    7    1
1026 1034  521  547  283  303  155  134   57   28    7    1
2050 2059 1034 1068  547  586  303  289  134   85   28    8    1
4098 4108 2059 2102 1068 1133  586  592  289  219   85   36    8    1
```

将每一行都逆序，并且最后一个值都减去$1$，得到

```
   1
   1    2
   1    3    3
   1    3    6    5
   1    4    6   11    9
   1    4   10   11   20   17
   1    5   10   21   20   37   33
   1    5   15   21   41   37   70   65
   1    6   15   36   41   78   70  135  129
   1    6   21   36   77   78  148  135  264  257
   1    7   21   57   77  155  148  283  264  521  513
   1    7   28   57  134  155  303  283  547  521 1034 1025
   1    8   28   85  134  289  303  586  547 1068 1034 2059 2049
   1    8   36   85  219  289  592  586 1133 1068 2102 2059 4108 4097
```

对于每一列（除了第$0$列）而言，从下面的数开始，都是两两出现，去掉其中一个，那么可以简化成：

```
(A)

 1  
 1  2  
 1  3  3  
 1  4  6  5  
 1  5 10 11  9  
 1  6 15 21 20 17 
 1  7 21 36 41 37 33 
 1  8 28 57 77 78 70 65 
```

可以发现，这个三角的产生方式和杨辉三角相同，只是边界值不一样。

舍去第一行，将其右上方进行补全，得到：

```
 1  2  1  1  1  1  1  1
 1  3  3  2  2  2  2  2
 1  4  6  5  4  4  4  4
 1  5 10 11  9  8  8  8
 1  6 15 21 20 17 16 16
 1  7 21 36 41 37 33 32
 1  8 28 57 77 78 70 65 
```

最终发现上面这个图形矩阵可以由杨辉三角的偏移叠加得到：

```
 1  0  0  0  0  0  0  0
 1  1  0  0  0  0  0  0
 1  2  1  0  0  0  0  0 
 1  3  3  1  0  0  0  0 
 1  4  6  4  1  0  0  0 
 1  5 10 10  5  1  0  0 
 1  6 15 20 15  6  1  0

 0  2  0  0  0  0  0  0
 0  2  2  0  0  0  0  0
 0  2  4  2  0  0  0  0
 0  2  6  6  2  0  0  0
 0  2  8 12  8  2  0  0
 0  2 10 20 20 10  2  0
 0  2 12 30 40 30 12  2

 0  0  1  0  0  0  0  0
 0  0  1  1  0  0  0  0
 0  0  1  2  1  0  0  0
 0  0  1  3  3  1  0  0
 0  0  1  4  6  4  1  0
 0  0  1  5 10 10  5  1
 0  0  1  6 15 20 15  6

 0  0  0  1  0  0  0  0
 0  0  0  1  1  0  0  0
 0  0  0  1  2  1  0  0
 0  0  0  1  3  3  1  0
 0  0  0  1  4  6  4  1
 0  0  0  1  5 10 10  5
 0  0  0  1  6 15 20 15

...
```

总之，$2^N$个子集中，$sg$函数值为$k$的子集个数为$f(N-k-1,\lceil\dfrac{k}{2}\rceil)$，其中$f(x,y)$表示三角形数组(A)一开始在第$x$列的第一个元素，然后再往下走$y$步后的元素。（注意当$k=0$时，需要将值添加回$1$。）

那么根据刚刚的思想，有

$$f(x,y)=C_{x+y-1}^y+\sum_{i=0}^x C_{x+y-1}^i$$

最终，使用等式$C_i^j=C_{i-1}^{j-1}+C_i^j$这个等式，在求$f(N-k-1,\lceil\dfrac{k}{2}\rceil)$时，将求和项的相邻两项合并。并且由于运算$\lceil\rceil$运算的存在，合并之后的结果也是连续的，通过这个现象可以$O(N)$维护出$f(N-k-1,\lceil\dfrac{k}{2}\rceil)$的所有值。最终使用快速沃尔什变换计算出最终答案。

## 代码

本代码参考了Thread中的内容并重新实现。

```C++
#include <bits/stdc++.h>
#include "tools.h"
using namespace std;
typedef long long ll;
const int N = 10000000;
const int M = 10000000;
ll mod=1000000007;
ll fac[N+4],inv[N+4],finv[N+4];
ll C(int n,int m){
    return fac[n]*finv[m]%mod*finv[n-m]%mod;
}
int main(){
    fac[0]=fac[1]=inv[1]=finv[0]=finv[1]=1;
    for(int i=2;i<=N;i++){
        fac[i]=fac[i-1]*i%mod;
        inv[i]=(mod-mod/i)*inv[mod%i]%mod;
        finv[i]=finv[i-1]*inv[i]%mod;
    }
    vector<int>b(N);
    b[0]=1;
    for(int k=1;k<N;k++){
        b[k]=(b[k-1]+C((N+k)/2-1,k))%mod;
        if(k>=2&&(N+k)%2==0) b[k]=(b[k]+b[k-2])%mod;
    }
    for(int k=0;k<N;k++)
        b[k]=(b[k]+C((N+k)/2-1,k-1))%mod;
    b[N-1]++;
    reverse(b.begin(),b.end());
    fwt.init_mod(mod);
    int ans=fwt.powXor(b,M)[0];
    printf("%d\n",ans);
}

```
