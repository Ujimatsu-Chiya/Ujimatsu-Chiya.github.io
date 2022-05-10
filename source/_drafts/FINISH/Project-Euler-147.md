---
title: Project Euler 147
tags:
  - Project Euler
mathja\times: true
---
<escape><!-- more --></escape>
    
    
# Project Euler 147
## 题目
### Rectangles in cross-hatched grids
In a $3\times2$ cross-hatched grid, a total of $37$ different rectangles could be situated within that grid as indicated in the sketch.

![](../images/p147.png)

There are $5$ grids smaller than $3\times2$, vertical and horizontal dimensions being important, i.e. $1\times1$, $2\times1$, $3\times1$, $1\times2$ and $2\times2$. If each of them is cross-hatched, the following number of different rectangles could be situated within those smaller grids:
$\begin{aligned}
1\times1&: 1 \\
2\times1&: 4 \\
3\times1&: 8 \\
1\times2&: 4 \\
2\times2&: 18
\end{aligned}$

Adding those to the $37$ of the $3\times2$ grid, a total of $72$ different rectangles could be situated within $3\times2$ and smaller grids.

How many different rectangles could be situated within $47\times43$ and smaller grids?


## 解决方案
假设该矩形大小为$n\times m(n\le m)$。

首先，和矩形边上平行的小矩形个数为$T(n,m)=\dfrac{n(n+1)m(m+1)}{4}$。

接下来考虑倾斜矩形的个数，使用了一些和多项式相关的小技巧。

合理猜测：这一类的矩形个数可以用多项式来表示，并且项的最高次数和上面一样，也是$4$。这种猜测个人认为比较合理，因为随着$n,m$的增长，两种方式矩形的增长速度感知上是相同的。

因此，假设这个公式为$p(n,m)=\sum_{i=0}^4\sum_{j=0}^{4-i}a_{i,j} n^im^j$.其中，多项式$a_{i,j}$是未知的，用待定系数求出来。

我首先写了一份比较暴力并且不美观的代码，用来计算小范围内的$p(n,m)$值：

```C++
# include <bits/stdc++.h>
using namespace std;
int solve(int n,int m){
    int o=max(n,m)*2;
    int ans=0;
    n<<=1;m<<=1;
    for(int i=0;i<=n;i++)
    for(int j=0;j<=m;j++){
        if((i+j)&1) continue;
        for(int d=1;d<=o;d++){
            int x=i-d,y=j+d;
            if(x<0||y>m) break;
            for(int k=1;k<=o;k++){
                if(max(k+i,k+x)<=n&&max(k+j,k+y)<=m) ++ans;
                else break;
            }
        }
    }
    return ans;
}
int main(){
    int M=7;
    for(int n=1;n<=M;n++)
        for(int m=n;m<=M;m++)
            printf("%d %d %d\n",n,m,solve(n,m));
}
```

用统计出来的$n,m,p(n,m)$，全部代入到公式$p(n,m)$中。由此构造出一个方程组。

使用sympy库的linsolve函数最终解出方程组，回代到公式，整合，也就是：

$\dfrac{n((2m-n)(4n^2-1)-3)}{6}$


最终把上面的第一种情况加起来即可。

不失一般性，如果$n>m$，那么将上面的式子的$n,m$两个变量进行交换。

本题甚至可以进一步整理公式直接导出答案$\sum_{i=1}^N\sum_{j=1}^M{T(i,j)+p(i,j)}$的通式，此处不赘述。

## 代码

```py
N, M = 47, 43


def solve(n, m):
    if n > m:
        n, m = m, n
    return n * (n + 1) * m * (m + 1) // 4 + n * ((2 * m - n) * (4 * n * n - 1) - 3) // 6


ans = 0
for i in range(1, N + 1):
    for j in range(1, M + 1):
        ans += solve(i, j)
print(ans)

```
