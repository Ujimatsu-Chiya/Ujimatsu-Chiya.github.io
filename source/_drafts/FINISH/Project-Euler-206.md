---
title: Project Euler 206
tags:
  - Project Euler
  - meet-in-the-middle
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 206
## 题目
### Concealed Square


Find the unique positive integer whose square has the form 1_2_3_4_5_6_7_8_9_0, where each “_” is a single digit.

## 解决方案

假设当前枚举的数位$n$。本题使用了如下剪枝方法：

1. 如果$n^2$最后一位是$0$，那么倒数第二位肯定也是$0$，故不考虑$n$的最低位$0$，直接舍去，在输出答案的时候恢复。
2. 需要枚举的$n$在$10^8$在$\sqrt{2}\times10^8$之间。因为$n^2$最高位为$1$，因此$10^{16}< n^2<2\times 10^{16}$。
3. 因此，$n$是一个$9$位数，最高位为$1$。使用meet-in-the-middle的思想进行枚举。一部分是枚举$n$的中间$3$位，最多$415$种情况，注意到这中间$3$位明显不能够对$n^2$的低$5$位产生影响；另一部分是枚举$n$的低$5$位，由于中间$3$位的平方数值不会不能影响$n^2$低$5$位的值，因此枚举的过程中，只保留平方数个位为$9$，百位为$8$，万位为$7$的情况。这低$5$位中的$100000$种只有$240$种情况是符合的。

排除了低$5$位的绝大多数情况后，最终枚举量其实很小。


## 代码

```py
ls = []
for i in range(100000):
    x = i * i % 100000
    if x % 10 == 9 and x // 100 % 10 == 8 and x // 10000 % 10 == 7:
        ls.append(i)

for l in range(415):
    for r in ls:
        x = 100000000 + l * 100000 + r
        if str(x * x)[::2] == "123456789":
            ans = x * 10
print(ans)

```