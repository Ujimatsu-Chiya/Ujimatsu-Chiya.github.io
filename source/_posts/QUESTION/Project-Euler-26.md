---
title: Project Euler 26
tags:
  - Project Euler
mathjax: true
date: 2022-04-27 09:56:19
---

<escape><!-- more --></escape>

# Project Euler 26
## 题目
### Reciprocal cycles
A unit fraction contains $1$ in the numerator. The decimal representation of the unit fractions with denominators $2$ to $10$ are given:

$$\begin{aligned}

\frac 1 2 &= 0.5\\\frac 1 3 &= 0.(3)\\\frac 1 4 &= 0.25\\\frac 1 5 &= 0.2\\\frac 1 6 &= 0.1(6)\\\frac 1 7 &= 0.(142857)\\\frac 1 8 &= 0.125\\\frac 1 9 &= 0.(1)\\\frac 1 {10} &= 0.1\\
\end{aligned}$$

Where $0.1(6)$ means $0.166666\ldots$, and has a $1$-digit recurring cycle. It can be seen that $\dfrac{1}{7}$ has a $6$-digit recurring cycle.

Find the value of $1000$ for which $\dfrac{1}{d}$ contains the longest recurring cycle in its decimal fraction part.

## 解决方案
做竖式除法，本质上是每次将上一次的结果作为余数，乘以$10$，填上被除数后面一位后（不过，本题的被除数只有一开始的1，往后都是$0$）的结果再做一次带余的整数除法。

在这道题，只要余数开始了循环，那么就可以根据上一次到达这个余数的时间计算周期。

以$\dfrac{2}{11}=0.181818\dots$为例。

$2* 10 \mod 11 = 9,\lfloor2 * 10 / 11\rfloor = 1$
$9* 10 \mod 11 = 2,\lfloor9 * 10 / 11\rfloor = 8$

余数$2$出现在了一开始的结果中，发生了循环，其长度为$2$。小数也计算了出来，分别为$1$和$8$。

因此，在这个数据范围下，循环节长度能以线性的时空复杂度计算出来。

## 代码

```C++
# include <bits/stdc++.h>
using namespace std;
const int N=1000;
int f[N+4];
int main(){
    int mx=0,ans=0;
    for(int x=2;x<N;x++){
        memset(f,-1,sizeof(f));
        int w=0;
        for(int j=1,k=0;j;j=j*10%x){
            if(f[j]!=-1){
                w=k-f[j];
                break;
            }
            f[j]=k++;
        }
        if(w>mx) mx=w,ans=x;
    }
    printf("%d\n",ans);
}
```