---
title: Project Euler 67
tags:
  - Project Euler
  - 动态规划
mathjax: true
date: 2022-04-30 10:32:20
---

<escape><!-- more --></escape>

# Project Euler 67

## 题目

### Maximum path sum II

By starting at the top of the triangle below and moving to adjacent numbers on the row below, the maximum total from top to bottom is $23$.
<center style="font-family:'Courier New',monospace;">
<font color=red>3</font><br/>
<font color=red>7</font> 4<br/>
2 <font color=red>4</font> 6<br/>
8 5 <font color=red>9</font> 3<br/>
</center>

That is, $3 + 7 + 4 + 9 = 23$.

Find the maximum total from top to bottom in [triangle.txt](../resources/p067_triangle.txt) (right click and ‘Save Link/Target As…’), a 15K text file containing a triangle with one-hundred rows.

**NOTE:** This is a much more difficult version of <a href="/18">Problem 18</a>. It is not possible to try every route to solve this problem, as there are 2^99 altogether! If you could check one trillion (10^12) routes every second it would take over twenty billion years to check them all. There is an efficient algorithm to solve it. ;o)

## 解决方案

本题的题解和第18题完全一致，只是读入做了改动。

## 代码

```C++
# include <bits/stdc++.h>
using namespace std;
const int N=15;
int t,f[N+4][N+4];
int main(){
    freopen("p067_triangle.txt","r",stdin);
    for(int i=1;i<=N;i++)
    for(int j=1;j<=i;j++){
        scanf("%d",&t);
        f[i][j]=max(f[i-1][j-1],f[i-1][j])+t;
    }
    printf("%d\n",*max_element(f[N]+1,f[N]+N+1));
}
```
