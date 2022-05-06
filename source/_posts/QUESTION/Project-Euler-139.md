---
title: Project Euler 139
tags:
  - Project Euler
mathjax: true
date: 2022-05-06 22:23:12
---

<escape><!-- more --></escape>
    

# Project Euler 139
## 题目
### Pythagorean tiles
Let $(a, b, c)$ represent the three sides of a right angle triangle with integral length sides. It is possible to place four such triangles together to form a square with length $c$.

For example, $(3, 4, 5)$ triangles can be placed together to form a $5$ by $5$ square with a $1$ by $1$ hole in the middle and it can be seen that the $5$ by $5$ square can be tiled with twenty-five $1$ by $1$ squares.

![](../images/p139.png)

However, if $(5, 12, 13)$ triangles were used then the hole would measure $7$ by $7$ and these could not be used to tile the $13$ by $13$ square.

Given that the perimeter of the right triangle is less than one-hundred million, how many Pythagorean triangles would allow such a tiling to take place?

## 本原勾股数组

[本原](https://mathworld.wolfram.com/PrimitivePythagoreanTriple.html)[勾股数组](https://mathworld.wolfram.com/PythagoreanTriple.html)，即一个正整数三元组$(a,b,c)$，满足$a^2+b^2+c^2\wedge\gcd(a,b,c)=1$。

通过枚举一系列的二元组$(s,t)$，其中$s>t\geq 1\wedge\gcd(s,t)=1,s,t$为奇数，可以不重不漏地产生本原勾股数组$(st,\dfrac{s^2-t^2}{2},\dfrac{s^2+t^2}{2})$。

## 解决方案

枚举产生出所有本原勾股数组$(a,b,c)$。可以知道，大正方形的边长为$c$，小正方形的边长为$b-a$。因此，只需判断$b-a$是否整除$c$。在此过程中也将非本原勾股数组进行统计。

## 代码

```C++
# include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N=100000000;
int main(){
    ll ans=0;
    for(int s=1;s*s+s<=N;s+=2){
        for(int t=1;t<s&&s*s+s*t<=N;t+=2){
            if(__gcd(s,t)==1){
                int a=s*t,b=(s*s-t*t)>>1,c=(s*s+t*t)>>1;
                if(c%(b-a)==0)
                    ans+=N/(a+b+c);
            }
        }
    }
    printf("%lld\n",ans);
}

```
