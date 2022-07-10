---
title: Project Euler 389
tags:
  - Project Euler
  - 概率
  - 动态规划
mathjax: true
---
<escape><!-- more --></escape>
    

# Project Euler 389
## 题目
### Platonic Dice

An unbiased single 4-sided die is thrown and its value, $T$, is noted.

$T$ unbiased $6$-sided dice are thrown and their scores are added together. The sum, $C$, is noted.

$C$ unbiased $8$-sided dice are thrown and their scores are added together. The sum, $O$, is noted.

$O$ unbiased $12$-sided dice are thrown and their scores are added together. The sum, $D$, is noted.

$D$ unbiased $20$-sided dice are thrown and their scores are added together. The sum, $I$, is noted.

Find the variance of $I$, and give your answer rounded to $4$ decimal places.


## 解决方案

不难想到使用动态规划解决本题。

当前先考虑一轮的过程：假设当前使用的是$m$面的骰子，那么令状态$g(i,j)(0\le j\le mi)$表示具有$i$个$m$面骰子的情况下，能够掷出$j$点的概率。

## 代码


```C++
# include <bits/stdc++.h>
using namespace std;
vector<int>d={4,6,8,12,20};
int main(){
    int m=1;
    vector<double>fp1(2);
    fp1[1]=1;
    for(int x:d){
        vector<double>fp2(1,1);
        vector<double>fn1(m*x+1,0);
        for(int i=1;i<=m;i++){
            vector<double>fn2(x*i+1+1);
            for(int j=0;j<=x*(i-1);j++){
                fn2[j+1]+=fp2[j]/x;
                fn2[j+x+1]-=fp2[j]/x;
            }
            for(int j=1;j<=x*i;j++){
                fn2[j]+=fn2[j-1];
            }
            fp2=fn2;
            for(int j=1;j<=x*i;j++)
                fn1[j]+=fp1[i]*fp2[j];
        }
        fp1=fn1;
        m*=x;
    }
    double ex1=0,ex2=0;
    for(int i=1;i<=m;i++){
        ex1+=fp1[i]*i;
        ex2+=fp1[i]*i*i;
    }
    double ans=ex2-ex1*ex1;
    printf("%.4f\n",ans);
}

```