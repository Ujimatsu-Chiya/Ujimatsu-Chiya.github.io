---
title: Project Euler 163
tags:
  - Project Euler
mathjax: true
date: 2022-05-24 11:02:10
---

<escape><!-- more --></escape>

# Project Euler 163

## 题目

### Cross-hatched triangles

Consider an equilateral triangle in which straight lines are drawn from each vertex to the middle of the opposite side, such as in the size $1$ triangle in the sketch below.

![](../images/p163.gif)

Sixteen triangles of either different shape or size or orientation or location can now be observed in that triangle. Using size $1$ triangles as building blocks, larger triangles can be formed, such as the size $2$ triangle in the above sketch. One-hundred and four triangles of either different shape or size or orientation or location can now be observed in that size $2$ triangle.

It can be observed that the size $2$ triangle contains $4$ size $1$ triangle building blocks. A size $3$ triangle would contain $9$ size $1$ triangle building blocks and a size $n$ triangle would thus contain $n^2$ size $1$ triangle building blocks.

If we denote $T(n)$ as the number of triangles present in a triangle of size $n$, then

$T(1) = 16$<br>
$T(2) = 104$

Find $T(36)$.

## 解决方案

为了避免答案因小数出现精度问题，我们决定将整个三角形进行拉伸变换，这将不会影响原来三角形的所有点、线相对位置。如下图所示，如果原来的单独一个等边三角形的边长为$2$，那么边长将拉伸到原来的$2$倍数；其高为$\sqrt{3}$，拉伸到原来的$2\sqrt{3}$倍长度。可以发现，这些点的坐标都已经变成了整数。

![](../images/p163-1.png)

为了将三角形的数量数出来，我们可以每次枚举三条**斜率不相同、不交于同一点的**一组的线段，然后判断它们的交点是否在大三角形内部或边上即可。

将前$4$项暴力枚举出来后，查询OEIS，发现结果为[A210687](https://oeis.org/A210687)。

在FORMULA一栏中，发现如下信息：

```
a(n) = (1678*n^3+3117*n^2+88*n-345*Mod[n,2]-320*Mod[n,3]-90*Mod[n,4]-288*Mod[n^3-n^2+n,5])/240. (Bill Daly)
```

这说明第答案为：
$$T(n)=\dfrac{1678n^3+3117n^2+88n-345\cdot(n\%2)-320\cdot(n\%3)-90\cdot(n\%4)-288\cdot ((n^3-n^2+n)\%5)}{240}$$

## 代码

```C++
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N=36;
struct P {
    ll x, y;
    // 向量减法
    P operator-(P p) const {
        return {x - p.x, y - p.y};
    }
    // 向量叉积
    ll operator^(P p) const {
        return x * p.y - y * p.x;
    }
    bool operator == (P &p) const{
        return x==p.x&&y==p.y;
    }
}p[3]={P{0,0},P{4*N,0},P{2*N,6*N}};
int m=0;
struct L {
    P p1, p2;
    // ax+by=c;
    ll a, b, c;
    L(){}
    L(P p1, P p2) {
        this->p1 = p1;
        this->p2 = p2;
        a = p1.y - p2.y;
        b = p2.x - p1.x;
        c = p1.x * (p1.y - p2.y) - p1.y * (p1.x - p2.x);
    }
}l[9*N+14];
bool in_triangle(P &q){
    bool neg=false,pos=false;
    for(int i=0;i<3;i++){
        ll w=(p[i]-q)^(p[(i+1)%3]-q);
        if(w>0) pos=true;
        if(w<0) neg=true;
    }
    return pos^neg;
}
bool solve(L &l1,L &l2, P &sol) {
    ll fm = l1.a * l2.b - l1.b * l2.a;
    if (fm == 0)
        return false;
    ll fx = l1.c * l2.b - l1.b * l2.c;
    ll fy = l1.a * l2.c - l1.c * l2.a;
    sol = P{fx/fm, fy/fm};
    return true;
}
int main() {
    for(int i=0;i<N;i++){
        l[++m]=L{P{4*i,0},P{4*i+2,6}};
        l[++m]=L{P{4*i+4,0},P{4*i+2,6}};
        l[++m]=L{P{2*i,6*i},P{2*i+4,6*i}};
    }
    int M=N-1;
    for(int i=0;i<2*N-1;i++){
        l[++m]=L{P{2*i+2,0},P{2*i+2,6}};
        l[++m]=L{P{i+1,3*i+3},P{0,4*i+4}};
    }
    for(int i=-M;i<=M;i++)
        l[++m]=L{P{4*i,0},P{4*i+6,6}};
    int ans=0;
    P a,b,c;
    for(int i=1;i<=m;i++){
        for(int j=i+1;j<=m;j++){
            if(!solve(l[i],l[j],a)) continue;
            for(int k=j+1;k<=m;k++){
                if(!solve(l[i],l[k],b)||!solve(l[j],l[k],c)) continue;
                if(a==b||b==c||a==c) continue;
                if(in_triangle(a)&&in_triangle(b)&&in_triangle(c))
                    ++ans;
            }
        }
    }
    printf("%d\n",ans);

}

```

```py
N = 36
ans = (1678 * N ** 3 + 3117 * N * N + 88 * N - N % 2 * 345 - N % 3 * 320 - N % 4 * 90 - (N ** 3 - N * N + N) % 5 * 288) // 240
print(ans)

```
