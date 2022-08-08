---
title: Project Euler 505
category:
  - Project Euler
tags:
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 505
## 题目
### Bidirectional Recurrence


Let:
<p style="margin-left:32px;">$\begin{array}{ll} x(0)&amp;=0 \\ x(1)&amp;=1 \\ x(2k)&amp;=(3x(k)+2x(\lfloor \frac k 2 \rfloor)) \text{ mod } 2^{60} \text{ for } k \ge 1 \text {, where } \lfloor \text { } \rfloor \text { is the floor function} \\ x(2k+1)&amp;=(2x(k)+3x(\lfloor \frac k 2 \rfloor)) \text{ mod } 2^{60} \text{ for } k \ge 1 \\ y_n(k)&amp;=\left\{{\begin{array}{lc} x(k) &amp;&amp; \text{if } k \ge n \\ 2^{60} - 1 - max(y_n(2k),y_n(2k+1)) &amp;&amp; \text{if } k < n \end{array}} \right. \\ A(n)&amp;=y_n(1) \end{array}$
You are given:
<p style="margin-left:32px;">$\begin{array}{ll} x(2)&amp;=3 \\ x(3)&amp;=2 \\ x(4)&amp;=11 \\ y_4(4)&amp;=11 \\ y_4(3)&amp;=2^{60}-9\\ y_4(2)&amp;=2^{60}-12 \\ y_4(1)&amp;=A(4)=8 \\ A(10)&amp;=2^{60}-34\\ A(10^3)&amp;=101881 \end{array}$
Find $A(10^{12})$.


# Project Euler 505
## 题目
### Bidirectional Recurrence

Let:<br>$x(0)=0$<br>$x(1)=1$<br>$x(2k)=(3x(k)+2x(\lfloor \frac k 2 \rfloor)) \text{ mod } 2^{60} \text{ for } k \ge 1 \text {, where } \lfloor \text { } \rfloor \text { is the floor function}$<br>$x(2k+1)=(2x(k)+3x(\lfloor \frac k 2 \rfloor)) \text{ mod } 2^{60} \text{ for } k \ge 1$<br>$y_n(k)=x(k) \text{ if } k \ge n$<br>$y_n(k)=2^{60} - 1 - max(y_n(2k),y_n(2k+1)) \text{ if } k < n$<br>$A(n)=y_n(1)$
You are given:<br>$x(2)=3$<br>$x(3)=2$<br>$x(4)=11$<br>$y_4(4)=11$<br>$y_4(3)=2^{60}-9$<br>$y_4(2)=2^{60}-12$<br>$y_4(1)=A(4)=8$<br>$A(10)=2^{60}-34$<br>$A(10^3)=101881$
Find $A(10^{12})$.


## 解决方案


## 代码


