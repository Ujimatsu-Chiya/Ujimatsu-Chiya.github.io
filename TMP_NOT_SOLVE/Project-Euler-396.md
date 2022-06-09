---
title: Project Euler 396
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 396
## 题目
### Weak Goodstein sequence


For any positive integer n, the <b>nth weak Goodstein sequence</b> {g_1, g_2, g_3, \dots} is defined as:
<ul><li> g_1 = <var>n</var>
</li><li> for <var>k</var> > 1, g_<var>k</var> is obtained by writing g_<var>k</var>-1 in base <var>k</var>, interpreting it as a base <var>k</var> + 1 number, and subtracting 1.
</li></ul>
The sequence terminates when g_<var>k</var> becomes 0.


For example, the 6th weak Goodstein sequence is {6, 11, 17, 25, \dots}:
<ul><li> g_1 = 6.
</li><li> g_2 = 11 since 6 = 110_2, 110_3 = 12, and 12 - 1 = 11.
</li><li> g_3 = 17 since 11 = 102_3, 102_4 = 18, and 18 - 1 = 17.
</li><li> g_4 = 25 since 17 = 101_4, 101_5 = 26, and 26 - 1 = 25.
</li></ul>
and so on.


It can be shown that every weak Goodstein sequence terminates.


Let G(<var>n</var>) be the number of nonzero elements in the <var>n</var>th weak Goodstein sequence.<br />
It can be verified that G(2) = 3, G(4) = 21 and G(6) = 381.<br />
It can also be verified that <span style="font-size:larger;"><span style="font-size:larger;">\sum</span></span> G(<var>n</var>) = 2517 for 1 \le <var>n</var> < 8.


Find the last 9 digits of <span style="font-size:larger;"><span style="font-size:larger;">\sum</span></span> G(<var>n</var>) for 1 \le <var>n</var> < 16.



# Project Euler 396
## 题目
### Weak Goodstein sequence

For any positive integer n, the <b>nth weak Goodstein sequence</b> {g_1, g_2, g_3, \dots} is defined as:
<ul>
<li>g_1 = n </li>
<li>for k > 1, g_k is obtained by writing g_k-1 in base k, interpreting it as a base k + 1 number, and subtracting 1.</li>
</ul>
The sequence terminates when g_k becomes 0.
For example, the 6th weak Goodstein sequence is {6, 11, 17, 25, \dots}:
<ul>
<li>g_1 = 6.</li>
<li>g_2 = 11 since 6 = 110_2, 110_3 = 12, and 12 - 1 = 11.</li>
<li>g_3 = 17 since 11 = 102_3, 102_4 = 18, and 18 - 1 = 17.</li>
<li>g_4 = 25 since 17 = 101_4, 101_5 = 26, and 26 - 1 = 25.<br>and so on.</li>
</ul>
It can be shown that every weak Goodstein sequence terminates.
Let G(n) be the number of nonzero elements in the nth weak Goodstein sequence.<br>It can be verified that G(2) = 3, G(4) = 21 and G(6) = 381.<br>It can also be verified that \sumG(n) = 2517 for 1 \le n < 8.
Find the last 9 digits of \sumG(n) for 1 \le n < 16.


## 解决方案


## 代码


