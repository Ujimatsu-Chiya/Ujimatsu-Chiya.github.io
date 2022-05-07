---
title: Project Euler 138
tags:
  - Project Euler
  - 佩尔方程
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 138
## 题目
### Special isosceles triangles


Consider the isosceles triangle with base length, $b = 16$, and legs, $L = 17$.

![](../images/p138.png)

By using the Pythagorean theorem it can be seen that the height of the triangle, $h = \sqrt{17^2 - 8^2} = 15$, which is one less than the base length.

With $b = 272$ and $L = 305$, we get $h = 273$, which is one more than the base length, and this is the second smallest isosceles triangle with the property that $h = b \pm 1$.

Find $\sum L$ for the twelve smallest isosceles triangles for which $h = b \pm 1$ and $b, L$ are positive integers.


## 解决方案

根据勾股定理，可以列出以下式子：

$$(\dfrac{b}{2})^2+h^2=L^2$$

代入$h=b\pm 1$，有$b^2+4(b\pm 1)^2=4L^2$

展开，得$5b^2\pm 8b+4=4L^2$

两边同乘以$5$，再配方，得$25b^2\pm 40b+16+4=20L^2$

移项，得$(5b\pm 4)^2-20L^2=-4$

两边同除$4$，有$(\dfrac{5b\pm4}{2})^2\pm5L^2=-1$。

令$x=\dfrac{5b\pm4}{2},y=L^2$，得到$x^2-5y^2=-1$，该类方程为负佩尔方程$x^2-Dy^2=-1$。

假设$x^2-Dy^2=-1$**存在**最小特解为$(x_1,y_1)$。那么，负佩尔方程的通解$(x_k,y_k)$由以下式子导出。

$$x_k+y_k\sqrt{D}=(x_{k-1}+y_{k-1}\sqrt{D})(x_1+y_1\sqrt{D})^2$$

容易发现，$x^2-5y^2=-1$的最小特解为$(2,1)$，代入上面的导出递推公式，得到通解递推公式：

$$\left \{\begin{aligned}
  & x_{k+1}=9x_k+20y_k\\
  & y_{k+1}=4x_k+9y_k
\end{aligned}\right.
$$

对于每个解，回代$b=\dfrac{2x\mp 4}{5}$，并判断$b$是否为一个正整数。

## 代码

```py
Q = 12
cnt = 0
x, y = 2, 1
ans = 0
while True:
    b05, b15 = 2 * x - 4, 2 * x + 4
    if b05 % 5 == 0 and b05 > 0 or b15 % 5 == 0:
        ans += y
        cnt += 1
        if cnt == Q:
            break
    x, y = 9 * x + 20 * y, 4 * x + 9 * y
print(ans)

```
