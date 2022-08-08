---
title: Project Euler 211
category:
  - Project Euler
tags:
mathjax: true
date: 2022-06-02 21:04:06
---

<escape><!-- more --></escape>

# Project Euler 211

## 题目

### Divisor Square Sum

For a positive integer $n$, let $\sigma_2(n)$ be the sum of the squares of its divisors. For example,

$$\sigma_2(10) = 1 + 4 + 25 + 100 = 130.$$

Find the sum of all $n, 0 < n < 64,000,000$ such that $\sigma_2(n)$ is a perfect square.

## 解决方案

在线性晒进行的过程中计算积性函数$\sigma_2$.筛出来的质数存放在数组$pr$中。

如果一个合数$i$使用了一个新质数$p$筛出来了一个新数$i\cdot p$，那么新数比原来的数多出来了一个质因子，和原来的答案是独立的，因此有$\sigma_2(i\cdot p)=\sigma(i)\cdot(p^2+1)$；否则，如果使用的是旧质数，那么按照上面的办法，新产生的一部分因子是重复的，而这一重复的部分恰好来自于$\sigma_2(i/p)$。以下图为例：

![](../images/p211-1.png)

黑色一行为当前数的质因子，蓝色的一行为因子平方和。$16$通过一个旧的质因子$2$筛出来了一个新数$32$。新构造的一部分因子平方，和原来$16$的一部分因子平方是重叠的（如图黄色部分），因此直接相加会导致重复。不难理解，这一重复部分完全可以用$8=16/2$的那一部分来表示，也就是$\sigma_2(i/p)\cdot p^2$。因此，这种情况下，$\sigma_2(i\cdot p)=\sigma_2(i)+(\sigma_2(i)-\sigma_2(i/p))p^2$来表示。

最终，直接判断所有计算出来的$\sigma_2$函数值是否为平方数即可。

## 代码

```C++
# include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N=64000000;
ll f[N+2],pr[N/4+400],v[N+2];
int m=0;
int main(){
    f[1]=1;
    for(int i=2;i<N;i++){
        if(v[i]==0){
            v[i]=i;f[i]=1ll*i*i+1;
            pr[++m]=i;
        }
        for(int j=1;j<=m;j++){
            if(pr[j]>v[i]||pr[j]>N/i) break;
            v[i*pr[j]]=pr[j];
            if(pr[j]==v[i]){
                f[i*pr[j]]=f[i]+(f[i]-f[i/pr[j]])*pr[j]*pr[j];
            }
            else{
                f[i*pr[j]]=f[i]*(pr[j]*pr[j]+1);
            }
        }
    }
    ll ans=0;
    for(int i=1;i<N;i++){
        ll sq=round(sqrt(f[i]));
        if(sq*sq==f[i]) ans+=i;
    }
    printf("%lld\n",ans);
}

```
