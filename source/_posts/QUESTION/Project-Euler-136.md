---
title: Project Euler 136
tags:
  - Project Euler
mathjax: true
date: 2022-05-06 22:23:07
---

<escape><!-- more --></escape>

# Project Euler 136

## 题目

### Singleton difference

The positive integers, $x, y$, and $z$, are consecutive terms of an arithmetic progression. Given that $n$ is a positive integer, the equation, $x^2 − y^2 − z^2 = n$, has exactly one solution when $n = 20$:

$$13^2 − 10^2 − 7^2 = 20$$

In fact there are twenty-five values of $n$ below one hundred for which the equation has a unique solution.

How many values of $n$ less than fifty million have exactly one solution?

## 解决方案

本题的解决方案和第135题完全一样，在这里不再赘述。

## 代码

```C++
# include <bits/stdc++.h>
using namespace std;
const int N=5e7,Q=1;
int c[N+4];
int main(){
    for(int z=1;z<=N;z++){
        for(int d=z/3+1;;d++){
            int w=(3*d-z)*(d+z);
            if(w>=N) break;
            c[w]+=1;
        }
    }
    int ans=0;
    for(int i=1;i<=N;i++)
        if(c[i]==Q) ++ans;
    printf("%d\n",ans);
}

```
