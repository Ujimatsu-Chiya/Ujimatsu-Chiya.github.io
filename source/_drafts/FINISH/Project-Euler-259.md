---
title: Project Euler 259
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>

# Project Euler 259

## 题目

### Reachable Numbers

A positive integer will be called *reachable* if it can result from an arithmetic expression obeying the following rules:

- Uses the digits 1 through 9, in that order and exactly once each.
- Any successive digits can be concatenated (for example, using the digits 2, 3 and 4 we obtain the number 234).
- Only the four usual binary arithmetic operations (addition, subtraction, multiplication and division) are allowed.
- Each operation can be used any number of times, or not at all.
- <dfn title="A minus sign applied to a single operand (as opposed to a subtraction operator between two operands)">Unary minus</dfn> is not allowed.
- Any number of (possibly nested) parentheses may be used to define the order of operations.

For example, $42$ is reachable, since $(1/23) *((4*5)-6) * (78-9) = 42$.

What is the sum of all positive reachable integers?

## 解决方案

本题的做法和区间动态规划的进行做法比较像。

如果现在要枚举$l,l+1,\dots,r-1,r$这一些数组成的表达式的值，并存放在集合$st[l][r]$中。那么我们可以对于$\forall k,l\le k< r$，枚举每个数$x\in st[l][k],y\in st[k+1][r]$，并将这些数通过任何一种运算，将运算结果（也就是$x+y,x-y,xy,x/y$）存放在集合$st[l][r]$中。当$y\neq 0$时才能做除法运算。

通过这种枚举方式，最终只需要判断集合$st[1][9]$存放的数是否为正整数即可。

为了方便和效率，本题没有采用分数进行实现，而是使用一个误差用于判断这个数是否为整数。另外，如果做除法时除数的绝对值大于$10^5$，那么不允许做（因为做出来的结果，无法用一个数乘回去，使得分母被消除）。

## 代码

```C++
#include <bits/stdc++.h>
typedef long long ll;
using namespace std;
const int M=9;
unordered_set<double>st[10][10];
unordered_set<int>ok;
double eps=1e-6;
int main(){
    for(int i=1;i<=M;i++){
        double w=0;
        for(int j=i;j<=M;j++){
            w=w*10+j;
            st[i][j].insert(w);
        }
    }
    for(int len=2;len<=M;len++){
        for(int l=1;l+len-1<=M;l++){
            int r=l+len-1;
            for(int k=l;k<r;k++){
                for(double vl:st[l][k]) for(double vr:st[k+1][r]){
                    st[l][r].insert(vl+vr);
                    st[l][r].insert(vl-vr);
                    st[l][r].insert(vl*vr);
                    if(abs(vr)>eps&&abs(vr)<100000)
                        st[l][r].insert(vl/vr);
                }
            }
        }
    }
    for(double x:st[1][M])
        if(abs(x-round(x))<eps){
            int w=round(x);
            if(w>0) ok.insert(w);
        }
    ll ans=0;
    for(int x:ok) ans+=x;
    printf("%lld\n",ans);
}

```
