---
title: Project Euler 581
category:
  - Project Euler
tags:
mathjax: true
date: 2022-07-13 22:57:14
---

<escape><!-- more --></escape>

# Project Euler 581

## 题目

### $47$-smooth triangular numbers

A number is $p$-smooth if it has no prime factors larger than $p$.

Let $T$ be the sequence of triangular numbers, ie $T(n)=\dfrac{n(n+1)}{2}$.

Find the sum of all indices $n$ such that $T(n)$ is $47$-smooth.

## Størmer 定理

[Størmer定理](https://en.wikipedia.org/wiki/St%C3%B8rmer%27s_theorem)，说明了上述定义的全体$P$-smooth数（注意这里的$P$是一个质数集合，比小于等于$p$的全体质数这种集合更普遍）中，连续两个数$n,n+1$都是$P$-smooth数的$n$的数量是有限的，并提供了一个算法查找这些$n$：

假设集合$P$的大小为$k$，其中最大的质数为$r$.

那么枚举由集合$P$中的质因子组合而成的所有无平方因子数$q$（一共有$2^k$个这样的$q$），然后解以下佩尔方程：

$$x^2-2qy^2=1$$

那么，对这个佩尔方程的前$\max\left(3,\dfrac{r+1}{2}\right)$个解$(x_i,y_i)$一一进行测试。如果$\dfrac{x_i+1}{2},\dfrac{x_i-1}{2}$都是$P$-smooth的，那么就找到了一个$P$-smooth对。

注意当$q=2$时，佩尔方程无解，因此需要规避这种情况。

## 解决方案

如果一个三角形数$\dfrac{n(n+1)}{2}$是$p$-smooth的，那么说明$n$和$n+1$是$p$-smooth的。

一开始的想法则是通过深度优先搜索直接产生所有$p$-smooth数$x$，并判断$x+1$是否为$p$-smooth数。并且拟定一个枚举上限$2\times 10^{12}$。

之后，我查阅了Størmer定理并直接解决本问题，至于佩尔方程的解法在66题已经详述。

不过，让我比较惊讶的是，Størmer定理的实现效率会比直接搜索更低。

OEIS上的数列[A002072](https://oeis.org/A002072)则给出了最大答案的上限。在`FORMULA`一栏中，找到

```
a(n) < 10^n/n except for n=4. (Conjectured, from experimental data.) - M. F. Hasler, Jan 16 2015
```

在实现Størmer定理时，还顺带了这个条件进行剪枝。

由于实现Størmer定理的效率过低，此处不附上使用它实现的代码。

## 代码

```C++
# include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const int M=47;
ll MX;
int pr[M+4],m=0,b[M+4];
ll ans=0;
void dfs(int f,ll x){
    if(f==m+1){
        ll y=x+1;
        for(int i=1;i<=m&&y>1;i++)
            while(y%pr[i]==0) y/=pr[i];
        if(y==1) ans+=x;
        return;
    }
    for(;x<=MX;x*=pr[f])
        dfs(f+1,x);
}
int main(){
    for(int i=2;i<=M;i++){
        if(b[i]) continue;
        pr[++m]=i;
        for(int j=i+i;j<=M;j+=i)
            b[j]=1;
    }
    MX=(m==4?4374:pow(10,m)/m);
    dfs(1,1);
    printf("%lld\n",ans);
}


```
