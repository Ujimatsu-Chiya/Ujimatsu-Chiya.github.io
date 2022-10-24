---
title: Project Euler 674
category:
  - Project Euler
tags:
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 674
## 题目
### Solving $\mathcal{I}$-equations


We define the $\mathcal{I}$ operator as the function
\[\mathcal{I}(x,y) = (1+x+y)^2+y-x\]
and $\mathcal{I}$-expressions as arithmetic expressions built only from variables names and applications of $\mathcal{I}$. A variable name may consist of one or more letters. For example, the three expressions $x$, $\mathcal{I}(x,y)$, and $\mathcal{I}(\mathcal{I}(x,ab),x)$ are all $\mathcal{I}$-expressions.

For two $\mathcal{I}$-expressions $e_1$ and $e_2$ such that the equation $e_1=e_2$ has a solution in non-negative integers, we define the least simultaneous value of $e_1$ and $e_2$ to be the minimum value taken by $e_1$ and $e_2$ on such a solution. If the equation $e_1=e_2$ has no solution in non-negative integers, we define the least simultaneous value of $e_1$ and $e_2$ to be $0$. For example, consider the following three $\mathcal{I}$-expressions:
\[\begin{array}{l}A = \mathcal{I}(x,\mathcal{I}(z,t))\\
B = \mathcal{I}(\mathcal{I}(y,z),y)\\
C = \mathcal{I}(\mathcal{I}(x,z),y)\end{array}\]
The least simultaneous value of $A$ and $B$ is $23$, attained for $x=3,y=1,z=t=0$. On the other hand, $A=C$ has no solutions in non-negative integers, so the least simultaneous value of $A$ and $C$ is $0$. The total sum of least simultaneous pairs made of $\mathcal{I}$-expressions from $\{A,B,C\}$ is $26$.

Find the sum of least simultaneous values of all $\mathcal{I}$-expressions pairs made of distinct expressions from file <a href="project/resources/p674_i_expressions.txt">I-expressions.txt</a> (pairs $(e_1,e_2)$ and $(e_2,e_1)$ are considered to be identical). Give the last nine digits of the result as the answer.



# Project Euler 674
## 题目
### Solving $\mathcal{I}$-equations

We define the $\mathcal{I}$ operator as the function<br>$$\mathcal{I}(x,y) = (1+x+y)^2+y-x$$<br>and $\mathcal{I}$-expressions as arithmetic expressions built only from variables names and applications of $\mathcal{I}$. A variable name may consist of one or more letters. For example, the three expressions $x$, $\mathcal{I}(x,y)$, and $\mathcal{I}(\mathcal{I}(x,ab),x)$ are all $\mathcal{I}$-expressions.
For two $\mathcal{I}$-expressions $e_1$ and $e_2$ such that the equation $e_1=e_2$ has a solution in non-negative integers, we define the least simultaneous value of $e_1$ and $e_2$ to be the minimum value taken by $e_1$ and $e_2$ on such a solution. If the equation $e_1=e_2$ has no solution in non-negative integers, we define the least simultaneous value of $e_1$ and $e_2$ to be $0$. For example, consider the following three $\mathcal{I}$-expressions:<br>$$\begin{array}{l}A = \mathcal{I}(x,\mathcal{I}(z,t))\<br>B = \mathcal{I}(\mathcal{I}(y,z),y)\<br>C = \mathcal{I}(\mathcal{I}(x,z),y)\end{array}$$<br>The least simultaneous value of $A$ and $B$ is $23$, attained for $x=3, y=1, z=t=0$. On the other hand, $A=C$ has no solutions in non-negative integers, so the least simultaneous value of $A$ and $C$ is $0$. The total sum of least simultaneous pairs made of $\mathcal{I}$-expressions from ${A,B,C}$ is $26$.
Find the sum of least simultaneous values of all $\mathcal{I}$-expressions pairs made of distinct expressions from file <a href="https://projecteuler.net/project/resources/p674_i_expressions.txt" target="_blank" rel="noopener">I-expressions.txt</a> (pairs $(e_1,e_2)$ and $(e_2,e_1)$ are considered to be identical). Give the last nine digits of the result as the answer.


## 解决方案


## 代码


