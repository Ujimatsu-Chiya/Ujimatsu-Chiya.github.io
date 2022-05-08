---
title: Project Euler 142
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 142
## 题目
### Perfect Square Collection
Find the smallest $x + y + z$ with integers $x > y > z > 0$ such that $x + y, x - y, x + z, x - z, y + z, y - z$ are all perfect squares.


## 解决方案

令这六个数分别为六个平方数
$\begin{aligned}
&x+y=a^2\\
&x-y=b^2\\
&x+z=c^2\\
&x-z=d^2\\
&y+z=e^2\\
&y-z=f^2
\end{aligned}$

将其中的一些式子相减，代入，可以得到以下式子：

$\begin{aligned}
&e^2=a^2-d^2\\
&f^2=a^2-c^2\\
&b^2=c^2-e^2\\
\end{aligned}$

我们最终枚举$a,c,e$三个值寻找答案，另外不难发现$a>c>e$。

由于本题的每个平方数的上限难以确定，故拟定为$10^6$。
## 代码


