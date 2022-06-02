---
title: Project Euler 229
tags:
  - Project Euler
mathjax: true
date: 2022-06-02 21:03:42
---

<escape><!-- more --></escape>

# Project Euler 229

## 题目

### Four Representations using Squares

Consider the number 3600. It is very special, because

$$\begin{aligned}
3600 &= 48^2 + 36^2 \\
3600 &= 20^2 + 2\times40^2 \\
3600 &= 30^2 + 3\times30^2 \\
3600 &= 45^2 + 7\times15^2 \\
\end{aligned}$$

Similarly, we find that $88201 = 99^2 + 280^2 = 287^2 + 2\times54^2 = 283^2 + 3\times52^2 = 197^2 + 7\times84^2$.

In 1747, Euler proved which numbers are representable as a sum of two squares.

We are interested in the numbers n which admit representations of all of the following four types:

$$\begin{aligned}
n &= a_1^2 + b_1^2\\
n &= a_2^2 + 2 b_2^2\\
n &= a_3^2 + 3 b_3^2\\
n &= a_7^2 + 7 b_7^2,\\
\end{aligned}$$

where the $a_k$ and $b_k$ are positive integers.

There are $75373$ such numbers that do not exceed $10^7$.

How many such numbers are there that do not exceed $2\times10^9$?

## 解决方案

为了节省空间，每次对$1\sim N$中连续分块的$M$个数暴力筛选。

因此，在枚举$a_k^2+kb^2_k$的过程中，需要有四个临时数组$l_k$来存储表示$b$枚举到哪里了。

同时，$M$的值必须比较大（如$N^{0.7}+1000$），不然筛选的过程会发生错误。

## 代码

```C++
# include <bits/stdc++.h>
using namespace std;
const int N=2000000000;
const int M= pow(N,0.7)+1000;
const int SQN=sqrt(N);
int l1[SQN+2],l2[SQN+2],l3[SQN+2],l7[SQN+2];
unsigned char used[M];
int main(){
    printf("%d\n",M);
    for(int i=1;i<=SQN;i++)
        l1[i]=l2[i]=l3[i]=l7[i]=1;
    int ans=0;
    for(int l=0,w,b;l<=N;l+=M) {
        int r = min(l + M, N + 1);
        for (int a = 1; a * a + l1[a] * l1[a] < r; a++) {
            for (b = l1[a]; (w = a * a + b * b) < r; b++)
                used[w - l] |= 1;
            l1[a] = b;
        }
        for (int a = 1; a * a + l2[a] * l2[a] * 2 < r; a++) {
            for (b = l2[a]; (w = a * a + b * b * 2) < r; b++)
                used[w - l] |= 2;
            l2[a] = b;
        }
        for (int a = 1; a * a + l3[a] * l3[a] * 3 < r; a++) {
            for (b = l3[a]; (w = a * a + b * b * 3) < r; b++)
                used[w - l] |= 4;
            l3[a] = b;
        }
        for (int a = 1; a * a + l7[a] * l7[a] * 7 < r; a++) {
            for (b = l7[a]; (w = a * a + b * b * 7) < r; b++)
                used[w - l] |= 8;
            l7[a] = b;
        }
        for (int i = l; i < r; i++) {
            if (used[i - l] == 15) ++ans;
            used[i - l] = 0;
        }
    }
    printf("%d\n",ans);
}
```
