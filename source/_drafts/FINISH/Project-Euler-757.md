---
title: Project Euler 757
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 757
## 题目
### Stealthy Numbers



A positive integer $N$ is *stealthy*, if there exist positive integers $a$, $b$, $c$, $d$ such that $ab = cd = N$ and $a+b = c+d+1$.

For example, $36 = 4\times 9 = 6\times 6$ is stealthy.


You are also given that there are 2851 stealthy numbers not exceeding $10^6$.


How many stealthy numbers  are there that don't exceed $10^{14}$?



## 解决方案

考虑

$\begin{aligned}
a&=xy\\
b&=(x+1)(y+1)\\
c&=x(y+1)\\
d&=y(x+1)\\
N&=x(x+1)y(y+1)
\end{aligned}$

那么由$x$和$y$通过构造出所有的$N$，接下来只需要对$N$进行去重即可。

## 代码


```C++
# include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const ll N=1e14;
int main(){
    vector<ll>v;
    for(ll x=1;x*(x+1)*x*(x+1)<=N;x++)
        for(ll y=x;x*(x+1)*y*(y+1)<=N;y++)
            v.push_back(x*(x+1)*y*(y+1));
    sort(v.begin(),v.end());
    int ans=unique(v.begin(),v.end())-v.begin();
    printf("%d\n",ans);
}

```