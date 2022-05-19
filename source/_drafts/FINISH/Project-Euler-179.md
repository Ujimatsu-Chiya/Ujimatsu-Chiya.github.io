---
title: Project Euler 179
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    

# Project Euler 179
## 题目
### Consecutive positive divisors

Find the number of integers $1 < n < 10^7$, for which $n$ and $n + 1$ have the same number of positive divisors. For example, $14$ has the positive divisors $1, 2, 7, 14$ while $15$ has $1, 3, 5, 15$.


## 解决方案

线性筛可以用于高速计算积性函数的值，本题需要求的积性函数是因数个数。

$v[i]$是$i$最小的质因数。如果用比$v[i]$更小的质因数$p$产生了一个新数，那么$i$中的所有因数都需要乘以一个$p$，与原来的因数一起成为新数的因子，因此多添加了一倍的因子。

如果$p=v[i]$，那么按照上面的说法，产生出来的因数是有重复的。假设$i$分解质因数后质因数$p$的次数为$e$，那么$p,p^2,\dots,p^e$都是重复的一部分，而这一部分因数的数量恰好和$\dfrac{i}{p}$因数数量相等，因此需要减去这一部分。

计算完因数个数函数后，直接进行判断。
## 代码


```C++
#include <bits/stdc++.h>
using namespace std;
const int N=1e7;
int pr[N/4+40],v[N+1],s[N+1],m=0;
int main(){
    s[1]=1;
    for(int i=2;i<=N;i++){
        if(v[i]==0){
            v[i]=i;s[i]=2;
            pr[++m]=i;
        }
        for(int j=1;j<=m;j++){
            if(pr[j]>v[i]||pr[j]>N/i) break;
            v[i*pr[j]]=pr[j];
            if(pr[j]==v[i])
                s[i*pr[j]]=s[i]+s[i]-s[i/pr[j]];
            else
                s[i*pr[j]]=s[i]+s[i];
        }
    }
    int ans=0;
    for(int i=1;i<N;i++)
        if(s[i]==s[i+1]) ++ans;
    printf("%d\n",ans);
}
```