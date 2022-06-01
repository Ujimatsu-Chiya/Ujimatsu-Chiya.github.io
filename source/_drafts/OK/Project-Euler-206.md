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
3. 因此，$n$是一个$9$位数，最高位为$1$。使用meet-in-the-middle的思想进行枚举。一部分是枚举$n$的中间$3$位，最多$415$种情况，注意到这中间$3$位明显不能够对$n^2$的低$5$位产生影响；另一部分是枚举$n$的低$5$位。

## 代码