---
title: Project Euler 224
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    

# Project Euler 224
## 题目
### Almost right-angled triangles II

Let us call an integer sided triangle with sides $a \le b \le c$ *barely obtuse* if the sides satisfy $a^2 + b^2 = c^2 - 1$.

How many barely obtuse triangles are there with perimeter $\le 75,000,000$?


## 解决方案

做法与223题完全一样，但是此时只有一棵树，并且树根为$(2,2,3)^T$。

## 代码

```C++
#include <bits/stdc++.h>
typedef long long ll;
using namespace std;
const int N = 75000000;
struct T{
    int a,b,c;
};
int main(){
    int ans=1;
    queue<T>q;
    q.push(T{2,2,3});
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