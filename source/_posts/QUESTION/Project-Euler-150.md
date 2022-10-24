---
title: Project Euler 150
category:
  - Project Euler
tags:
mathjax: true
date: 2022-05-10 13:47:49
---

<escape><!-- more --></escape>

# Project Euler 150

## 题目

### Searching a triangular array for a sub-triangle having minimum-sum

In a triangular array of positive and negative integers, we wish to find a sub-triangle such that the sum of the numbers it contains is the smallest possible.

In the example below, it can be easily verified that the marked triangle satisfies this condition having a sum of $-42$.

![](../images/p150.gif)

We wish to make such a triangular array with one thousand rows, so we generate 500500 pseudo-random numbers s_k in the range ±2^19, using a type of random number generator (known as a Linear Congruential Generator) as follows:

$\begin{aligned}
&t := 0 \\
&\text{for }k = 1 \text{ up to } k = 500500: \\
&\quad t := (615949*t + 797807) \text{ modulo } 2^{20} \\
&\quad s_k := t-2^{19} \\
\end{aligned}$

Thus: $s_1 = 273519, s_2 = -153582, s_3 = 450905$ etc

Our triangular array is then formed using the pseudo-random numbers thus:

$$s_1$$
$$s_2\ s_3$$
$$s_4\ s_5\ s_6 $$
$$s_7\ s_8\ s_9\ s_{10}$$
$$\dots$$

Sub-triangles can start at any element of the array and extend down as far as we like (taking-in the two elements directly below it from the next row, the three elements directly below from the row after that, and so on).

The “sum of a sub-triangle” is defined as the sum of all the elements it contains.

Find the smallest possible sub-triangle sum.

## 解决方案

将数字三角形直接转化成一个以左下角为顶点的直角三角形，方便存储。如下：

$$\begin{aligned}
& s_1 \\
& s_2\ s_3\\
& s_4\ s_5\ s_6 \\
& s_7\ s_8\ s_9\ s_{10}\\
& \dots
\end{aligned}$$

那么令三角形的行数为$n$，设$a[i][j](1\le j\le i\le n)$表示第$i$行第$j$列的数。

假设$s(i,j)=\sum_{k=1}^ja[i][k]$，也就是求出每一行的前缀和。其中，$s(i,0)=0$。

那么，对于最上面的点$(i,j)$，直角边长为$d(i+d-1\le  n)$的三角形的和为：$f(i,j,d)=\sum_{k=0}^{d-1} s(i+k,j+k)-s(i+k,j-1)$。

可以看出，当$d\ge 2$时，$f(i,j,d)=f(i,j,d-1)+s(i+d-1,j+d-1)-s(i+d,j-1)$.

由上式可以提供一种做法：先枚举最上面的点$(i,j)$，然后从小到大枚举三角形的边长$d$，枚举到第$d$次时，就将第$i+d-1$行第$j$列之后的$d$个数直接加起来。

这种做法需要枚举$\Theta(n^3)$个小三角形。但本人能力有限，还没想到$O(n^2)$的算法。（如果想到了就补上）

## 代码

```C++
# include <bits/stdc++.h>
# define mem(a,b) memset(a,b,sizeof(a))
using namespace std;
typedef long long ll;
const int N=1000;
ll s[N+4][N+4];
ll ans=0;
int main(){
    ll b=1<<19,t=0;
    for(int i=1;i<=N;i++)
    for(int j=1;j<=i;j++){
        t=(615949ll*t+797807)%(b*2);
        s[i][j]=s[i][j-1]+(t-b);
    }
    for(int i=1;i<=N;i++){
        for(int j=1;j<=i;j++){
            ll sum=0;
            for(int d=0;i+d<=N;d++){
                sum+=s[i+d][j+d]-s[i+d][j-1];
                ans=min(ans,sum);
            }
        }
    }
    printf("%lld\n",ans);
}

```
