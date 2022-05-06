---
title: Project Euler 112
tags:
  - Project Euler
  - 模拟
mathjax: true
date: 2022-05-06 22:24:01
---

<escape><!-- more --></escape>
    
# Project Euler 112
## 题目
### Bouncy numbers


Working from left-to-right if no digit is exceeded by the digit to its left it is called an increasing number; for example, $134468$.

Similarly if no digit is exceeded by the digit to its right it is called a decreasing number; for example, $66420$.

We shall call a positive integer that is neither increasing nor decreasing a "bouncy" number; for example, $155349$.

Clearly there cannot be any bouncy numbers below one-hundred, but just over half of the numbers below one-thousand ($525$) are bouncy. In fact, the least number for which the proportion of bouncy numbers first reaches $50\%$ is $538$.

Surprisingly, bouncy numbers become more and more common and by the time we reach $21780$ the proportion of bouncy numbers is equal to $90\%$.

Find the least number for which the proportion of bouncy numbers is exactly $99\%$.



## 解决方案

可以发现，随着$n$的增大，弹跳数的数量会占绝大多数。

因此，直接从$1$开始暴力枚举，并直接判断是否为弹跳数。

## 代码

```C++
# include <bits/stdc++.h>
using namespace std;
const int M=99;
int main(){
    int ans,cnt=0;
    for(int i=1;;i++){
        string s=to_string(i);
        bool u=0,d=0;
        for(int i=0;i+1<s.size()&&!(u&&d);i++){
            if(s[i]<s[i+1]) u=1;
            if(s[i]>s[i+1]) d=1;
        }
        if(u&&d) ++cnt;
        if(cnt*100==M*i){
            ans=i;
            break;
        }
    }
    printf("%d\n",ans);
}

```

