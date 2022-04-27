---
title: Project Euler 18
tags:
  - Project Euler
  - 动态规划
mathjax: true
date: 2022-04-27 09:55:45
---

<escape><!-- more --></escape>
# Project Euler 18 
## 题目
### Maximum path sum I

By starting at the top of the triangle below and moving to adjacent numbers on the row below, the maximum total from top to bottom is $23$.
<center style="font-family:'Courier New',monospace;">
<font color=red>3</font><br/>
<font color=red>7</font> 4<br/>
2 <font color=red>4</font> 6<br/>
8 5 <font color=red>9</font> 3<br/>
</center>

That is, $3 + 7 + 4 + 9 = 23$.

Find the maximum total from top to bottom of the triangle below:
<center style="font-family:'Courier New',monospace;">
75<br />
95 64<br />
17 47 82<br />
18 35 87 10<br />
20 04 82 47 65<br />
19 01 23 75 03 34<br />
88 02 77 73 07 63 67<br />
99 65 04 28 06 16 70 92<br />
41 41 26 56 83 40 80 70 33<br />
41 48 72 33 47 32 37 16 94 29<br />
53 71 44 65 25 43 91 52 97 51 14<br />
70 11 33 28 77 73 17 78 39 68 17 57<br />
91 71 52 38 17 14 91 43 58 50 27 29 48<br />
63 66 04 68 89 53 67 30 73 16 69 87 40 31<br />
04 62 98 27 23 09 70 98 73 93 38 53 60 04 23<br />
</center>

**NOTE:** As there are only $16384$ routes, it is possible to solve this problem by trying every route. However, <a href="/67">Problem 67</a>, is the same challenge with a triangle containing one-hundred rows; it cannot be solved by brute force, and requires a clever method! ;o)

## 解决方案

将数字三角形直接转化成一个以左下角为顶点的直角三角形，存在p018.txt中，方便读取：

<left style="font-family:'Courier New',monospace;">
75<br />
95 64<br />
17 47 82<br />
18 35 87 10<br />
20 04 82 47 65<br />
19 01 23 75 03 34<br />
88 02 77 73 07 63 67<br />
99 65 04 28 06 16 70 92<br />
41 41 26 56 83 40 80 70 33<br />
41 48 72 33 47 32 37 16 94 29<br />
53 71 44 65 25 43 91 52 97 51 14<br />
70 11 33 28 77 73 17 78 39 68 17 57<br />
91 71 52 38 17 14 91 43 58 50 27 29 48<br />
63 66 04 68 89 53 67 30 73 16 69 87 40 31<br />
04 62 98 27 23 09 70 98 73 93 38 53 60 04 23<br />
</left>

此时可以将问题转化为：要么向下走，要么向右下角走。

本题将用到动态规划算法。

令$n=15$，其中$n$表示数字三角形的大小。
记录状态$f(i,j)(1\leq j\leq i\leq n)$为：当前走到第$i$行第$j$列的数的情况下，可以得到的路径最大和是多少，用$a[i][j]$表示第$i$行第$j$列的数。

那么，可以得到状态转移方程：

$$
f(i,j)= 
\left \{\begin{aligned}
  &a[i][j]  & & \mathrm{if\quad} i=j=1 \\
  &f(i-1,j-1)+a[i][j] & & \mathrm{else if\quad} j=i \\
  &f(i-1,j)+a[i][j] & & \mathrm{else if\quad} j=1 \\
  &\max(f(i-1,j-1),f(i-1,j)) + a[i][j] & & \mathrm{otherwise}
\end{aligned}\right.
$$

最后的答案则是$\max_{j=1}^nf(n,j)$.

## 代码

```C++
```C++
# include <bits/stdc++.h>
using namespace std;
const int N=15;
int t,f[N+4][N+4];
int main(){
    freopen("p018.txt","r",stdin);
    for(int i=1;i<=N;i++)
    for(int j=1;j<=i;j++){
        scanf("%d",&t);
        f[i][j]=max(f[i-1][j-1],f[i-1][j])+t;
    }
    printf("%d\n",*max_element(f[N]+1,f[N]+N+1));
}
```