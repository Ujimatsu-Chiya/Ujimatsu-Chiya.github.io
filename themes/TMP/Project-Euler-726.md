---
title: Project Euler 726
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 726
## 题目
### Falling bottles


Consider a stack of bottles of wine. There are $n$ layers in the stack with the top layer containing only one bottle and the bottom layer containing $n$ bottles. For $n=4$ the stack looks like the picture below.

<div class="center">
<img src="project/images/p726_FallingBottles.jpg" class="dark_img" alt="" /></div>

The <i>collapsing process</i> happens every time a bottle is taken. A space is created in the stack and that space is filled according to the following recursive steps:
<ul><li>No bottle touching from above: nothing happens. For example, taking $F$.</li>
<li>One bottle touching from above: that will drop down to fill the space creating another space. For example, taking $D$.</li>
<li>Two bottles touching from above: one will drop down to fill the space creating another space. For example, taking $C$.</li>
</ul>
This process happens recursively; for example, taking bottle $A$ in the diagram above. Its place can be filled with either $B$ or $C$. If it is filled with $C$ then the space that $C$ creates can be filled with $D$ or $E$. So there are 3 different collapsing processes that can happen if $A$ is taken, although the final shape (in this case) is the same.


Define $f(n)$ to be the number of ways that we can take all the bottles from a stack with $n$ layers. 
Two ways are considered different if at any step we took a different bottle or the collapsing process went differently.


You are given $f(1) = 1$, $f(2) = 6$ and $f(3) = 1008$.

Also define
<div class="center">
$\displaystyle	S(n) = \sum_{k=1}^n f(k)$</div>

Find $S(10^4)$ and give your answer modulo $1\,000\,000\,033$.



# Project Euler 726
## 题目
### Falling bottles

Consider a stack of bottles of wine. There are $n$ layers in the stack with the top layer containing only one bottle and the bottom layer containing $n$ bottles. For $n=4$ the stack looks like the picture below.
<img src="https://projecteuler.net/project/images/p726_FallingBottles.jpg" alt="">
The <i>collapsing process</i> happens every time a bottle is taken. A space is created in the stack and that space is filled according to the following recursive steps:
<ul>
<li>No bottle touching from above: nothing happens. For example, taking $F$.</li>
<li>One bottle touching from above: that will drop down to fill the space creating another space. For example, taking $D$.</li>
<li>Two bottles touching from above: one will drop down to fill the space creating another space. For example, taking $C$.</li>
</ul>
This process happens recursively; for example, taking bottle $A$ in the diagram above. Its place can be filled with either $B$ or $C$. If it is filled with $C$ then the space that $C$ creates can be filled with $D$ or $E$. So there are $3$ different collapsing processes that can happen if $A$ is taken, although the final shape (in this case) is the same.
Define $f(n)$ to be the number of ways that we can take all the bottles from a stack with $n$ layers. Two ways are considered different if at any step we took a different bottle or the collapsing process went differently.
You are given $f(1) = 1$, $f(2) = 6$ and $f(3) = 1008$.
Also define<br>$$\displaystyle    S(n) = \sum_{k=1}^n f(k)$$
Find $S(10^4)$ and give your answer modulo $1\ 000\ 000\ 033$.


## 解决方案


## 代码


