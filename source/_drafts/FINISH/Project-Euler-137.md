---
title: Project Euler 137
tags:
  - Project Euler
  - 佩尔方程
  - OEIS
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 137
## 题目
### Fibonacci golden nuggets


Consider the infinite polynomial series $A_F(x) = x F_1 + x^2 F_2 + x^3 F_3 + \dots$, where $F_k$ is the $k$th term in the Fibonacci sequence: $1, 1, 2, 3, 5, 8, \dots$; that is, $F_k = F_{k-1} + F_{k-2}$, $F_1 = 1$ and $F_2 = 1$.

For this problem we shall be interested in values of $x$ for which $A_F(x)$ is a positive integer.

Surprisingly 
$\begin{aligned} 
A_F(\tfrac{1}{2})
 & = (\tfrac{1}{2})\times 1 + (\tfrac{1}{2})^2\times 1 + (\tfrac{1}{2})^3\times 2 + (\tfrac{1}{2})^4\times 3 + (\tfrac{1}{2})^5\times 5 + \cdots \\ 
 & = \tfrac{1}{2} + \tfrac{1}{4} + \tfrac{2}{8} + \tfrac{3}{16} + \tfrac{5}{32} + \cdots \\
 & = 2
\end{aligned}$

The corresponding values of $x$ for the first five natural numbers are shown below.

|$x$|$A_F(x)$|
|-|-|
|$\sqrt{2}-1$|$1$|
|$\dfrac{1}{2}$|$2$|
|$\dfrac{\sqrt{13}-2}{3}$|$3$|
|$\dfrac{\sqrt{89}-5}{8}$|$4$|
|$\dfrac{\sqrt{34}-3}{5}$|$5$|

We shall call $A_F(x)$ a golden nugget if $x$ is rational, because they become increasingly rarer; for example, the $10\mathrm{th}$ golden nugget is $74049690$.

Find the $15\mathrm{th}$ golden nugget.


## 解决方案
对$A_F(x)$的等号两边乘以一个$x$，再和原式相乘，有
$$
\begin{aligned}
A_F(x)      & =xF_1+    & x^2F_2+x^3F_3+\dots \\
xA_F(x)     & =         & x^2F_1+x^3F_2+\dots\\
(1+x)A_F(x) &=xF_1+ &x^2F_3+x^3F_4+\dots\\
\end{aligned}
$$

将$A_F(x)$代入第三条式子，有： 

$$
(1+x)A_F(x)=xF_1+\dfrac{A_F(x)}{x}-F_1-xF_2
$$

代入$F_1=F_2=1$，化简后，有：

$A_F(x)=\dfrac{x}{1-x-x^2}$

令$A_F(x)=n$，$n$是一个正整数，有：$x=n(1-x-x^2)$

化成关于$x$的一元二次方程，有$nx^2+(n+1)x-n=0$

如果$x$是一个有理数，那么其判别式$\Delta$必须是有理数。也就是$(n+1)^2-4n^2=5n^2+2n+1$必须是一个平方数。

因此，令正整数$y$满足$y^2=5n^2+2n+1$。

两边乘以$5$，并配方，得$25n^2+10n+1+4=5y^2$

移项，得：$(5n+1)^2-5y^2=-4$

令$x=5n+1$，那么得到$x^2-5y^2=-4$，该类方程为[广义佩尔方程](https://en.wikipedia.org/wiki/Pell%27s_equation#Generalized_Pell's_equation)：$x^2-Dy^2=N$。

如果广义佩尔方程存在解，那么广义佩尔方程就存在无数个解。

但是，广义佩尔方程的基础解有多个，不像$N=1,-1$时的情形。

求解广义佩尔方程的解一般是PQA算法和Lagrange-Matthews-Mollin(LMM)算法，鉴于我能力有限，我无法详细描述怎么不重不漏地求基础解。

接下来介绍怎么产生通解：

我们使用一个办法来根据基础解$x^2-Dy^2=N$的一个解$(x_1,y_1)$，产生对应的通解：

假设$(a_k,b_k)$为佩尔方程$x^2-Dy^2=1$的一组解，那么，将两个式子$x_1^2-Dy_1^2=N,a_k^2-Db_k^2=1$左右两边相乘，有：

$(x_1^2-Dy_1^2)(a_k^2-Db_k^2)=N$

可以将上式子转化成$(x_1a_k+Dy_1b_k)^2-D(x_1b_k+y_1a_k)^2=N$

那么就构造出了方程$x^2-Dy^2=N$的一组新解$(x_1a_k+Dy_1b_k,x_1b_k+y_1a_k)$。

因此根据一组基础解，可以构造出一组通解：

$$\left \{\begin{aligned}
  & x_{k+1}=x_1a_k+Dy_1b_k\\
  & y_{k+1}=y_1a_k+x_1b_k
\end{aligned}\right.
$$


回到题目本身，可以发现，$x^2-5y=-4$有三组基础解$(-1,1),(1,1),(4,2)$。分别将这三组基础解代入到上面的公式，分别有

$$\left \{\begin{aligned}
  & x_{k+1}=-a_k+5b_k\\
  & y_{k+1}=a_k-b_k
\end{aligned}\right.
$$

$$\left \{\begin{aligned}
  & x_{k+1}=a_k+5b_k\\
  & y_{k+1}=a_k+b_k
\end{aligned}\right.
$$

$$\left \{\begin{aligned}
  & x_{k+1}=4a_k+10b_k\\
  & y_{k+1}=2a_k+4b_k
\end{aligned}\right.
$$

再根据66题的算法，可以得到$x^2-5y^2=1$的解：
$$a_1=9,b_1=4$$
$$\left \{\begin{aligned}
  & a_{k+1}=9a_k+20b_k\\
  & b_{k+1}=4a_k+9b_k
\end{aligned}\right.
$$

将求出的$x$回代$n=\dfrac{x-1}{5}$。第$15$小的正整数$n$为所求。

如果将该数列前几项用来查询OEIS，结果为[A081018](https://oeis.org/A081018)。

以下标题信息，说明第$n$个斐波那契金块是第$2n$和$2n+1$项的斐波那契数的乘积。
```
Fibonacci(2n)*Fibonacci(2n+1)
```

## 代码


```py
N = 15


def gen_solution():
    x1, y1, x2, y2, x3, y3 = -1, 1, 1, 1, 4, 2
    a, b = 9, 4
    for x in (x1, x2, x3):
        yield x
    while True:
        x1, y1 = -a + 5 * b, a - b
        x2, y2 = a + 5 * b, a + b
        x3, y3 = 4 * a + 10 * b, 2 * a + 4 * b
        for x in (x1, x2, x3):
            yield x
        a, b = 9 * a + 20 * b, 4 * a + 9 * b


ls = []
for x in gen_solution():
    if x > 2 and (x - 1) % 5 == 0:
        ls.append((x-1)//5)
    if len(ls) == N:
        break

ans = ls[-1]
print(ans)
```

```py
N = 15
a, b = 1, 1
for i in range(2 * N - 1):
    a, b = b, a + b
ans = a * b
print(ans)
```