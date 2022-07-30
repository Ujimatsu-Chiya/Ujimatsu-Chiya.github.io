---
title: Project Euler 560
tags:
  - Project Euler
  - SG定理
  - 快速沃尔什变换
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 560
## 题目
### Coprime Nim


Coprime Nim is just like ordinary normal play Nim, but the players may only remove a number of stones from a pile  that is **coprime** with the current size of the pile. Two players remove stones in turn. The player who removes the last stone wins.

Let $L(n, k)$ be the number of **losing** starting positions for the first player, assuming perfect play, when the game is played with $k$ piles, each having between $1$ and $n - 1$ stones inclusively.

For example, $L(5, 2) = 6$ since the losing initial positions are $(1, 1), (2, 2), (2, 4), (3, 3), (4, 2)$ and $(4, 4)$.

You are also given $L(10, 5) = 9964, L(10, 10) = 472400303, L(10^3, 10^3)  \mod 1 000 000 007 = 954021836$.

Find $L(10^7, 10^7) \mod 1 000 000 007$

## 快速沃尔什变换

目标：给定两个长度为$N=2^n$的序列$a,b$（两个序列从下标从$0$开始），求一个长度为$N$的序列$c$，满足：

$$c_k=\sum_{i \circ j=k} a_i\cdot b_j$$

其中运算符$\circ$是三种位运算的运算符之一：与运算$\&$，或运算$|$，异或运算$\oplus$。

快速沃尔什变换可以将整个计算过程的时间复杂度从$O(N^2)$下降到$O(N \log N)$。

此处不详述这个算法，[此处](https://zhuanlan.zhihu.com/p/65998145)为参考文章和代码。

## 解决方案

令$N=10^7,K=10^7$。

可以看出这是一个公平组合游戏，我们将每一堆石头视为独立的一个游戏局面，使用SG定理来解决本题。这里的石头一共有$K$堆，第$i$堆一共有$a_i$个，那么整个游戏的$sg$函数值为$sg(a_1)\oplus sg(a_2)\oplus\dots sg(a_k)$。

考虑目前的某一堆石头，一共有$n$个，每一次操作是取出$d$个石头，其中$\gcd(n,d)=1$。因此，可以写出一堆石头的$sg$函数定义：

$$
sg(n)=
\left \{\begin{aligned}
  &0 & & \mathrm{if\quad} n=0 \\
  &\text{mex}(\{sg(n-d)|\gcd(i,d)=1\}) & & \mathrm{else}
\end{aligned}\right.
$$

其中运算$\text{mex}(s)$表示集合$s$中未出现的最小的非负整数。

那么考虑运行这一份代码，打印出前一部分项的$sg$函数。

```C++
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N=100,M=100;
int sg[N+4];
bool mex[M+4];
int pr[N/10+100],v[N+4];
int main(){
    for(int i=1;i<=N;i++){
        memset(mex,0,sizeof(mex));
        for(int j=1;j<=i;j++)
            if(__gcd(i,j)==1) mex[sg[i-j]]=1;
        int j=0;
        for(;mex[j];++j);
        sg[i]=j;
        printf("%d %d\n",i,sg[i]);
    }
}

```

发现规律如下：

- $sg(1)=1$
- 如果$n$为偶数，那么$sg(n)=0$
- 否则，假设$n$的最小质因子为$p$，如果质数表中第$k$个质数（$k$从$1$开始算起）为$p$，那么$sg(n)=k$。

最终问题转化为有多少种方法可以将$sg$函数值填入一个长度为$K$的序列，并且这$K$个值的异或和为$0$。

令状态$g(i,j)(0\le i\le K,j\ge 0)$表示填入长度为$i$的序列，并且异或和为$j$的方案数有多少个。那么不难写出状态转移方程为：

$$
g(i,j)=
\left \{\begin{aligned}
  &1  & & \mathrm{if\quad} i=0\wedge j=0 \\
  &0 & & \mathrm{else if\quad} i=0 \\
  &\sum_{k} g(i-1,j\oplus k) \cdot c[k] & & \mathrm{else}
\end{aligned}\right.
$$

注意到，此时$sg$函数值比较大，可以达到$O(\dfrac{N}{\log N})$的级别。

但是，对于$Q$这种数据范围而言，直接进行转移效率非常低。

如果我们已经求出了长度为$a$的序列的各种填法$g(a,\cdot)$和长度为$b$的各种填法$g(b,\cdot)$，不难知道我们可以通过卷积组合出$g(a+b,\cdot)$。

枚举所有的$g(a,i)$和$g(b,j)$，将这两部分值直接合并起来：

$g(a,i)\cdot g(b,j)\rightarrow g(a+b,i\oplus j)$

直接枚举这两部分的值效率非常低，可以使用快速沃尔什变换加速计算这两部分的合并。

因此，这给了我们一个方案：依次求出$g(2^0,\cdot),g(2^1,\cdot),g(2^2,\cdot),\dots$。然后针对$Q$，选择这些求出的$g(2^i,\cdot)$进行合并即可。

最终答案为$g(Q,0)$。


## 代码

为了加速，特地设计了一个powXor的函数。如果直接按照上面的快速沃尔什变换模板使用，那么总共需要做$O(\log Q)$次变换和逆变换。而此处由于是多次求值，因此总共只需要$3$次变换和逆变换。

```C++
# include <bits/stdc++.h>
# include "tools.h"
using namespace std;
typedef long long ll;
const int N=10000000,M=10000000;
int mod= 1000000007;
int pr[N/5+100],v[N+4],m=0;
int main(){
    for(int i=2;i<=N;i++){
        if(v[i]==0){
            pr[++m]=i;v[i]=m;
        }
        for(int j=1;j<=m;j++){
            if(j>v[i]||pr[j]>N/i) break;
            v[i*pr[j]]=j;
        }
    }
    v[1]=1;
    for(int i=2;i<=N;i+=2)
        v[i]=0;
    vector<int>b(m+1);
    for(int i=1;i<N;i++)
        ++b[v[i]];
    fwt.init_mod(mod);
    int ans=fwt.powXor(b,M)[0];
    printf("%d\n",ans);
}

```