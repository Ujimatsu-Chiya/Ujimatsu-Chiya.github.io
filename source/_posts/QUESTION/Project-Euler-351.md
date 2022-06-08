---
title: Project Euler 351
tags:
  - Project Euler
mathjax: true
date: 2022-06-08 22:37:49
---

<escape><!-- more --></escape>

# Project Euler 351

## 题目

### Hexagonal orchards

A *hexagonal orchard* of order $n$ is a triangular lattice made up of points within a regular hexagon with side $n$. The following is an example of a hexagonal orchard of order $5$:

![](../images/p351_hexorchard.png)

Highlighted in green are the points which are hidden from the center by a point closer to it. It can be seen that for a hexagonal orchard of order $5, 30$ points are hidden from the center.

Let $H(n)$ be the number of points hidden from the center in a hexagonal orchard of order $n$.

$H(5) = 30.\ H(10) = 138.\ H(1 000) = 1177848.$

Find $H(100 000 000)$.

## 解决方案

我们考虑将整个图形建立坐标系进行分析。

以正右为$x$轴正方向，以$x$轴逆时针旋转$120°$的为$y$轴正方向，那么可以建立一个平面坐标系，每一个点都有一个整数的坐标。

然后，将$y$轴顺时针旋转$30°$，所有的点的位置跟着变化，那么整个$5$阶六边形图像就变成了以下模样：

![](../images/p351-1.png)

其中，绿色是被遮挡的点。

对于原来的六边形，由于六片中，每一片都是平等的，因此我们只考虑$x$轴逆时针旋转$60°$这一片的计算，而这一片在新的坐标中则对应着上图中蓝色三角形的那一部分，我们只考虑的点是$(x,y)$，其中$1\le y\le x\le n$。

如果一个点$(x,y)$被遮挡了，那么$\gcd(x,y)>1$，因为点$(\dfrac{x}{\gcd(x,y)},\dfrac{y}{\gcd(x,y)})$一定在线段$(0,0)-(x,y)$上。

因此，计算出所有没有被遮挡的点，它们的个数为

$$\sum_{i=1}^n\sum_{j=1}^i[\gcd(i,j)=1]=\sum_{i=1}^n\varphi(i)$$

其中，$[]$表示示性函数，表示$[]$里面的值是否为真，如果为真，那么值为$0$，否则值为$1$。$\varphi$表示为欧拉函数。

那么，蓝色三角形中未被遮挡的点的数量为$\dfrac{n(n+1)}{2}-\sum_{i=1}^n\varphi(i)$。

因此，

$$H(n)=3n(n+1)-6\sum_{i=1}^n\varphi(i)$$

## 代码

```C++
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N=1e8;
int pr[N+4],v[N+4],m=0;
int phi[N+4];
int main(){
    phi[1]=1;
    for(int i=2;i<=N;i++){
        if(v[i]==0){
            v[i]=i;phi[i]=i-1;pr[++m]=i;
        }
        for(int j=1;j<=m;j++){
            if(pr[j]>v[i]||pr[j]>N/i) break;
            v[i*pr[j]]=pr[j];
            phi[i*pr[j]]=phi[i]*(v[i]==pr[j]?pr[j]:pr[j]-1);
        }
    }
    ll sum=0;
    for(int i=1;i<=N;i++)
        sum+=phi[i];
    sum = 1ll*N*(N+1)/2-sum;
    ll ans=sum*6;
    printf("%lld\n",ans);
}
```
