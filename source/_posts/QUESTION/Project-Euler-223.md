---
title: Project Euler 223
category:
  - Project Euler
tags:
mathjax: true
date: 2022-06-18 21:59:26
---

<escape><!-- more --></escape>

# Project Euler 223

## 题目

### Almost right-angled triangles I

Let us call an integer sided triangle with sides $a \le b \le c$ *barely acute* if the sides satisfy $a^2 + b^2 = c^2 + 1$.

How many barely acute triangles are there with perimeter $\le 25,000,000$?

## 解决方案

[本原勾股数组树](https://en.wikipedia.org/wiki/Tree_of_primitive_Pythagorean_triples)是一种数据结构，如果已知一个本原勾股数组$t=(a,b,c)^T$，那么可以通过以下方式产生三个不同的本原勾股数组：构造三个矩阵，分别为

$${\displaystyle {\begin{array}{lcr}
A={\begin{bmatrix}1&-2&2\\2&-1&2\\2&-2&3\end{bmatrix}}&
B={\begin{bmatrix}1&2&2\\2&1&2\\2&2&3\end{bmatrix}}&
C={\begin{bmatrix}-1&2&2\\-2&1&2\\-2&2&3\end{bmatrix}}
\end{array}}}$$

那么，$At,Bt,Ct$分别是产生的三个不同的本原勾股数组。产生的本原勾股数组可以继续使用该方法继续产生新的本原勾股数组，从而整个结构构成了一课**三叉树**。

它同时还介绍了，如果树根是$(3,4,5)^T$，那么产生的本原勾股数组是**不重不漏**的。

经过验证，如果$a^2+b^2=c^2+1$，上面的矩阵仍然是可用的（也就是说，如果已知$a^2+b^2=c^2+1$，那么产生的新$(a',b',c')$也满足$a'^2+b'^2=c'^2+1$）。但是需要注意枚举过程中，$a$和$b$有可能是相等的，三个产生分支需要去掉其中一个。

经过小范围枚举，一共有两棵树，树根为$(1,1,1)$和$(1,2,2)。$

本代码采用的是广度优先搜索，避免递归深度太大导致栈溢出。

该[页面](https://mathworld.wolfram.com/PythagoreanTriple.html)也介绍了本原勾股数组树的一部分内容，事实上，本代码实现采用的是这个页面中的矩阵。

## 代码

```C++
#include <bits/stdc++.h>
typedef long long ll;
using namespace std;
const int N = 25000000;
struct T{
    int a,b,c;
};
int main(){
    int ans=2;
    queue<T>q;
    q.push(T{1,1,1});
    q.push(T{1,2,2});
    while(!q.empty()){
        T t=q.front();q.pop();
        int a=t.a,b=t.b,c=t.c;
        int x=a-2*b+2*c,y=2*a-b+2*c,z=2*a-2*b+3*c;
        if(x+y+z<=N){
            ++ans;q.push(T{x,y,z});
        }
        x=-a+2*b+2*c,y=-2*a+b+2*c,z=-2*a+2*b+3*c;
        if(a!=b&&x+y+z<=N){
            ++ans;q.push(T{x,y,z});
        }
        x=2*a+b+2*c,y=a+2*b+2*c,z=2*a+2*b+3*c;
        if(x+y+z<=N){
            ++ans;q.push(T{x,y,z});
        }
    }
    printf("%d\n",ans);
}
```
