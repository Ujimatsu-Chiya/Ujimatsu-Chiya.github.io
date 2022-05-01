---
title: Project Euler 74
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>

# Project Euler 74
## 题目
### Digit factorial chains
The number $145$ is well known for the property that the sum of the factorial of its digits is equal to $145$:
$$1! + 4! + 5! = 1 + 24 + 120 = 145$$
Perhaps less well known is $169$, in that it produces the longest chain of numbers that link back to $169$; it turns out that there are only three such loops that exist:
$$\begin{aligned}
& 169 \rightarrow 363601 \rightarrow 1454 \rightarrow 169 \\ 
& 871 \rightarrow 45361 \rightarrow 871\\
& 872 \rightarrow 45362 \rightarrow 872
\end{aligned}$$

It is not difficult to prove that EVERY starting number will eventually get stuck in a loop. For example,

$$\begin{aligned}
& 69 \rightarrow 363600 \rightarrow 1454 \rightarrow 169 \rightarrow 363601 (\rightarrow 1454)\\
& 78 \rightarrow 45360 \rightarrow 871 \rightarrow 45361 (\rightarrow 871)\\
& 540 \rightarrow 145 (\rightarrow 145)
  \end{aligned}$$

Starting with $69$ produces a chain of five non-repeating terms, but the longest non-repeating chain with a starting number below one million is sixty terms.

How many chains, with a starting number below one million, contain exactly sixty non-repeating terms?

## 解决方案

根据题目可以看到，有些数经过多次变换后，就会陷入一个循环，不会回到自身了。

因此，本代码实现时，考虑了这个当前数是在环上还是在链上。如果是在环上，那么需要记录循环节和周期。如果是在链上，取下一轮迭代的结果进行加$1$即可。

本代码采用了记忆化搜索，每个值的后继都只会被计算一次。

## 代码
```C++
# include <bits/stdc++.h>
using namespace std;
const int N=1000000,M=60;
int f[N<<2],fac[14];
int st[N<<2],pos[N<<2];
int dfs(int u,int fl){
    st[fl]=u;
    if(f[u]) return f[u];
    if(pos[u])
        return f[u]=fl-pos[u];
    pos[u]=fl;
    int s=0;
    for(int k=u;k;k/=10)
        s+=fac[k%10];
    int x=dfs(s,fl+1);
    pos[u]=0;
    if(f[u]) return f[u];
    else return f[u]=x+1;
}
int main(){
    fac[0]=1;
    for(int i=1;i<10;i++)
        fac[i]=fac[i-1]*i;
    int ans=0;
    for(int i=1;i<=N;i++)
        if(dfs(i,1)==M) ++ans;
    printf("%d\n",ans);
}
```
