---
title: Project Euler 28
tags:
  - Project Euler
  - OEIS
mathjax: true
date: 2022-04-27 09:56:27
---

<escape><!-- more --></escape>


# Project Euler 28
## 题目
### Number spiral diagonals
Starting with the number $1$ and moving to the right in a clockwise direction a $5$ by $5$ spiral is formed as follows:

<center style="font-family: 'Lucida Consolas', 'Consolas', 'Courier New', monospace">
<span style="color:red"><b>21</b></span> 22 23 24 <span style="color:red"><b>25</b></span><br />
20 &nbsp;<span style="color:red"><b>7</b></span> &nbsp;8  <span style="color:red"><b>&nbsp;9</b></span> 10<br />
19  &nbsp;6  &nbsp;<span style="color:red"><b>1</b></span>  &nbsp;2 11<br />
18  &nbsp;<span style="color:red"><b>5</b></span>  &nbsp;4  &nbsp;<span style="color:red"><b>3</b></span> 12<br />
<span style="color:red"><b>17</b></span> 16 15 14 <span style="color:red"><b>13</b></span>
</center>

It can be verified that the sum of the numbers on the diagonals is $101$.
What is the sum of the numbers on the diagonals in a $1001$ by $1001$ spiral formed in the same way?

## 解决方案

容易观察到，从里面向外，每一个圈都会比里面的一个圈多$8$个元素。（以上图为例，第$1$个圈为$1$，第$2$个圈为$2\sim9$，第$3$个圈为$10\sim25$）。

因此，在第$n$个圈中，四个角上的数可以分别用一个二次多项式$p(n)=an^2+bn+c$来定义这个通项公式。

这里不再详细计算。

通过OEIS查询，可以发现：

右下角的通项公式为[A054554](https://oeis.org/A054554)，$4n^2-10n+7$;
左下角的通项公式为[A053755](https://oeis.org/A053755)，$4(n-1)^2+1$;
左上角的通项公式为[A054569](https://oeis.org/A054569)，$4n^2-6n+3$;
右上角的通项公式为$(2n-1)^2$

直接取所有值相加。

也可以再用平方和公式进一步导出结果：$\dfrac{2}{3}(8n^3-9n^2+7n)-3$

## 代码

NOTE: 本代码只适用于矩阵大小为奇数时的情况。
```Python
N = 1001
ans = 0

# 1~N/2+1：从内向外的圈数。
for i in range(1, N // 2 + 2):
    ans += 4 * i * i - 10 * i + 7
    ans += 4 * (i - 1) * (i - 1) + 1
    ans += 4 * i * i - 6 * i + 3
    ans += (2 * i - 1) ** 2
# 中心点算重复了3次，故减去。
ans -= 3
print(ans)
```

```Python
N = 1001
N = N // 2 + 1
ans = (8 * N ** 3 - 9 * N ** 2 + 7 * N) * 2 // 3 - 3
print(ans)
```