---
title: Project Euler 195
category:
  - Project Euler
tags:
mathjax: true
date: 2022-05-19 21:56:42
---

<escape><!-- more --></escape>

# Project Euler 195

## 题目

### Inscribed circles of triangles with one angle of $60$ degrees

Let’s call an integer sided triangle with exactly one angle of $60$ degrees a 60-degree triangle.

Let $r$ be the radius of the inscribed circle of such a $60$-degree triangle.

There are $1234$ $60$-degree triangles for which $r \le 100$.

Let $T(n)$ be the number of $60$-degree triangles for which $r \le n$, so $T(100) = 1234, T(1000) = 22767$ and $T(10000) = 359912$.

Find $T(1053779)$.

## 解决方案

令$N=1053379$。根据余弦定理，假设三角形两边为长度$a,b$，第三条边的长度$c$，其对角为$60°$，那么$a,b,c$满足：

$$a^2+b^2-ab=c^2$$

这篇[文章](http://www.geocities.ws/fredlb37/node9.html)提到了一种构造出一组**本原**三元组$(a,b,c)$（即$\gcd(a,b,c)=1$）满足$a^2+b^2-ab=c^2$的方法：如果$m>n,\gcd(n,m)=1,3 \nmid (m-n)$,那么有：

$$a=2mn+n^2,b=2mn+m^2,c=m^2+n^2+mn\qquad(1)$$

或者是

$$a=m^2-n^2,b=2mn+m^2,c=m^2+n^2+mn\qquad(2)$$

根据等积法，不难发现内切圆的半径$r$满足$\dfrac{a+b+c}{2}\cdot r=\dfrac{1}{2}ab\sin 60°$。

分别代入式$(1),(2)$，分别得到

$$r=\dfrac{\sqrt{3}mn}{2}\qquad(3)$$

$$r=\dfrac{(m-n)(2n+m)}{2\sqrt{3}}\qquad(4)$$

因此，根据$(3)(4)$式枚举出所有$r\le N$的本原三元组后，计算对应非本原三元组的数量即可。

## 代码

```C++
#include <bits/stdc++.h>
using namespace std;
const int N = 1053779;
double eps=1e-8;
double sq3=sqrt(3);
int main() {
    int ans = 0;
    for (int m = 1; 0.5 * sq3 * m <= N; m++) {
        double r;
        for (int n = 1; n < m && (r = 0.5 * sq3 * m * n - eps) <= N; n++) {
            if ((m - n) % 3 && __gcd(m, n) == 1) {
                ans += int(1.0 * N / r + eps);
            }
        }
    }
    double c = 0.5 / sq3;
    for (int n = 1; c * (2 * n + 1) <= N; n++) {
        double r;
        for (int m = n + 1; (r = c * (m - n) * (2 * n + m)  - eps) <= N; m++) {
            if ((m - n) % 3 && __gcd(m, n) == 1) {
                ans += int(1.0 * N / r + eps);
            }
        }
    }
    printf("%d\n", ans);
}
```
