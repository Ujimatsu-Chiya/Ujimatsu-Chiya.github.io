---
title: Project Euler 210
category:
  - Project Euler
tags:
mathjax: true
date: 2022-06-18 21:58:59
---

<escape><!-- more --></escape>

# Project Euler 210

## 题目

### Obtuse Angled Triangles

Consider the set $S(r)$ of points $(x,y)$ with integer coordinates satisfying |$x| + |y| \le r$.

Let $O$ be the point $(0,0)$ and $C$ the point $(\dfrac{r}{4},\dfrac{r}{4})$.

Let $N(r)$ be the number of points $B$ in $S(r)$, so that the triangle $OBC$ has an obtuse angle, i.e. the largest angle $\alpha$ satisfies $90°<\alpha<180°$.

So, for example, $N(4)=24$ and $N(8)=100$.

What is $N(1,000,000,000)$?

## 解决方案

本解决方案只适用于$r$为$8$的倍数的情况。

这些点一共由三部分组成，以$r=8$为例，如下图所示：

![](../images/p210-1.png)

其中，位于直线$x-y=0$上的点都不是合法的，因为$\triangle OBC$此时是一个退化的三角形。接下来的计算将忽略这些点。

那么一共有三种情况：

1. $\angle O$为钝角。这些点位于平面$x+y<0$中，有$r^2$个。
2. $\angle C$为钝角。这些点位于平面$x+y>\dfrac{r}{2}$中，有$\dfrac{r^2}{2}$个。
3. $\angle B$为钝角。这些点位于平面$(x-\dfrac{r}{8})^2+(y-\dfrac{r}{8})^2<\dfrac{r^2}{32}$中，也就是一个圆内。

接下来重点是计算情况3中的点个数。

令$s=\dfrac{r}{8}$，那么此时$s$是一个整数。这个圆的圆心也就是$(s,s)$。

将圆心挪到原点，此时等价于求圆$x^2+y^2=2s^2$内有多少个点，这部分点一共有

$$2\cdot{\lfloor\sqrt{2s^2-1}\rfloor}+\sum_{x=1}^{\lfloor\sqrt{2s^2-1}\rfloor}(4\cdot\lfloor\sqrt{2s^2-x^2-1}\rfloor+2)-2(s-1)$$

注意最后一项是在直线$x-y=0$上的点，一共有$2(s-1)$个，这些点需要去掉。

## 代码

```C++
#include <bits/stdc++.h>
typedef long long ll;
using namespace std;
const ll N=1e9;
int main(){
    ll ans=3ll*N*N/2;
    ll s=N>>3;
    ll r2=s*s*2;
    for(ll x=0,y=sqrt(r2)+1;x*x<=r2;x++){
        for(;y>=0&&x*x+y*y>=r2;--y);
        if(x==0) ans+=y*2;
        else if(y>=0) ans+=y*4+2;
    }
    ans-=2*(s-1);
    printf("%lld\n",ans);
}
```
