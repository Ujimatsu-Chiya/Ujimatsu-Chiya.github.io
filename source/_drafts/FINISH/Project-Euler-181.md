---
title: Project Euler 181
tags:
  - Project Euler
  - 动态规划
  - OEIS
mathjax: true
---
<escape><!-- more --></escape>
    

# Project Euler 181
## 题目
### Investigating in how many ways objects of two different colours can be grouped

Having three black objects B and one white object W they can be grouped in 7 ways like this:

||||||||
|-|-|-|-|-|-|-|
|(BBBW)|(B,BBW)|(B,B,BW)|(B,B,B,W)|(B,BB,W)|(BBB,W)|(BB,BW)|

In how many ways can sixty black objects B and forty white objects W be  thus grouped?


## 解决方案

令$N=60,M=40$。不难发现，一个**非空**的内部组合一共有$O=(N+1)(M+1)-1$种不同情况。

为了使得计数不重不漏，我们规定了一种内部组合的”顺序“，其中第$k(k\le O)$种内部组合包含了$x[k]$个黑色物体，$y[k]$个白色物体。

如果第$k$种内部组合已经出现了，那么以后就只能使用$k,k+1,\dots,O$的内部组合，不能再使用以前的组合。

那么，使用动态规划的方法进行计数。令$f(i,j,k)(0\le i\le N,0\le j\le M,0\le k\le O)$表示已经使用了$i$个黑色物体和$j$个白色物体，内部组合使用序号已经到达了$k$的情况。


$$
f(i,j,k)=
\left \{\begin{aligned}
  &1 & & \mathrm{if\quad} i=0\&j=0 \\
  &0 & & \mathrm{else if\quad} k=0 \\
  &f(i,j,k-1)+f(i-x[k],j-y[k],k) & & \mathrm{else if\quad} i\ge x[k]\&j\ge y[k] \\
  &f(i,j,k-1) & & \mathrm{else}
\end{aligned}\right.
$$

注意，$k=0$时说明还没使用过任何一种内部组合，但是$i+j>0$。这明显是不可能的，因此这些状态赋值为$0$。

对于方程的第二行，如果当前使用的黑白物体数量都能够凑成一个第$k$内部组合，那么就可以找到上一轮的状态，产生第$k$种内部组合，到达当前状态。

同时，每一个状态可以什么都不需要做，直接继承上一个状态的结果。

最终答案为$f(N,M,O)$。

将结果的前几项查询OEIS，发现结果为[A054225](https://oeis.org/A054225)。

找到FORMULA一栏，发现如下信息：

```
G.f.: Product_{ i=1..infinity, j=0..i} 1/(1-x^(i-j)*y^j).
```

这说明了，它们的数量的二维序列可以写成一个二元生成函数：

$$G(x,y)=\prod_{k=1}^{\infty}\prod_{j=0}^k\dfrac{1}{1-x^{k-j}y^j}$$

其中，$x^Ny^M$的系数即为所求答案。
## 代码


```C++
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N=60,M=40;
const int O=(N+1)*(M+1)-1;
ll f[N+1][M+1][O+4];
int x[O+4],y[O+4];
int main() {
    for (int i = 0, p = 0; i <= N; i++)
        for (int j = 0; j <= M; j++, p++) {
            x[p] = i;
            y[p] = j;
        }
    for (int j = 1; j <= O; j++)
        f[0][0][j] = 1;
    for (int i = 0; i <= N; i++) {
        for (int j = 0; j <= M; j++) {
            if (i == 0 && j == 0) continue;
            for (int k = 1; k <= O; k++) {
                f[i][j][k] = f[i][j][k - 1];
                if (x[k] <= i && y[k] <= j)
                    f[i][j][k] += f[i - x[k]][j - y[k]][k];
            }
        }
    }
    ll ans = f[N][M][O];
    printf("%lld\n", ans);
}

```