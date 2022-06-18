---
title: Project Euler 246
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    

# Project Euler 246
## 题目
### Tangents to an ellipse

A definition for an ellipse is:

Given a circle $c$ with centre $M$ and radius $r$ and a point $G$ such that $d(G,M)<r$, the locus of the points that are equidistant from $c$ and $G$ form an ellipse.

The construction of the points of the ellipse is shown below.

![](../images/p246_anim.gif)

Given are the points $M(-2000,1500)$ and $G(8000,1500)$. 

Given is also the circle $c$ with centre $M$ and radius $15000$.

The locus of the points that are equidistant from $G$ and $c$ form an ellipse $e$.

From a point $P$ outside $e$ the two tangents $t_1$ and $t_2$ to the ellipse are drawn.

Let the points where $t_1$ and $t_2$ touch the ellipse be $R$ and $S$.

![](../images/p246_ellipse.gif)

For how many lattice points $P$ is angle $RPS$ greater than $45$ degrees?


## 解决方案

$|EG|=|EU|$，$|EU|+|EM|=r$，因此$|EG|+|EM|=r=2a$，其中$2a$是椭圆的长轴长度，焦距$2c=d(G,M)$。由于椭圆的中心也在个点，那么为了方便处理问题，将椭圆的中心挪到原点，那么可以写成椭圆的标准方程：

$$\dfrac{x^2}{a^2}+\dfrac{y^2}{b^2}=1$$

其中$a=7500,c=5000,b^2=a^2-c^2$。

那么，由于椭圆关于两个坐标轴对称，因此只考虑第一象限以及$x,y$轴正半轴上的格点。

对于圆外任意一点$P(x_0,y_0)$，那么该点的点斜式方程为$y-y_0=k(x-x_0)$，那么和椭圆方程联立，得到一个关于$x$的一元二次方程：

$$(a^2k^2+b^2)x^2+(2a^2ky_0x-2a^2k^2x_0)x+a^2y_0^2-2a^2kx_0y_0+a^2k^2x_0^2-a^2b^2=0$$

由于所求直线为切线，因此令其$\Delta=0$，得到关于$k$的一元二次方程：

$$(x_0^2 - a^2)k^2-2x_0y_0k+y_0^2-b^2=0$$

也就是说，$k$不同的两个解对应着直线的斜率，不失一般性，假设其分别为$k_0,k_1,k_0<k_1$。

这两条直线夹角的正切值为$\dfrac{k_1-k_0}{1+k_0k_1}$。

解决本题时，还采用了一个假设：当$\angle RPS=45°$时，$P$点的轨迹$\Gamma$是一个凸曲线。

## 代码


```py
from math import ceil, sqrt
from itertools import count

Mx, My = -2000, 1500
Gx, Gy = 8000, 1500
R = 15000
a = R / 2
c = ((Mx - Gx) ** 2 + (My - Gy) ** 2) ** 0.5 / 2
a2 = a ** 2
b2 = a2 - c ** 2
eps = 1e-10
cnt2 = cnt4 = 0
pre_r = int((a + 4) * (a + 4))

for x0 in count(0, 1):
    if x0 != a:
        if x0 < a:
            y0 = ceil(sqrt(b2 * (1 - x0 * x0 / a2)) - eps)
        else:
            y0 = 0
        l = y0
        r = pre_r
        while l < r:
            mid = (l + r + 1) >> 1
            A = x0 * x0 - a2
            B = -2 * x0 * mid
            C = mid * mid - b2
            D = B * B - 4 * A * C
            k = [(-B - sqrt(D)) / (2 * A), (-B + sqrt(D)) / (2 * A)]
            tg = (k[1] - k[0]) / (1 + k[0] * k[1])
            if 0 < tg <= 1:
                r = mid - 1
            else:
                l = mid
        if l == 0:
            break
        if x0 == 0:
            cnt2 += l - y0 + 1
        elif y0 > 0:
            cnt4 += l - y0 + 1
        else:
            cnt4 += l
            cnt2 += 1
        pre_r = l
    else:
        y0 = 1
        while True:
            k = (y0 * y0 - b2) / (2 * x0 * y0)
            if k >= 1:
                break
            cnt4 += 1
            y0 += 1
ans = cnt2 * 2 + cnt4 * 4
print(ans)

```