---
title: Project Euler 220
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    


# Project Euler 220
## 题目
### Heighway Dragon

Let $\mathbf{D}_0$ be the two-letter string “Fa”. For $n\ge1$, derive $\mathbf{D}_n$ from $\mathbf{D}_{n-1}$ by the string-rewriting rules:

“a” → “aRbFR”<br>“b” → “LFaLb”

Thus, $\mathbf{D}_0$ = “Fa”, $\mathbf{D}_1$ = “FaRbFR”, $\mathbf{D}_2$ = “FaRbFRRLFaLbFR”, and so on.

These strings can be interpreted as instructions to a computer graphics program, with “F” meaning “draw forward one unit”, “L” meaning “turn left $90$ degrees”, “R” meaning “turn right $90$ degrees”, and “a” and “b” being ignored. The initial position of the computer cursor is $(0,0)$, pointing up towards $(0,1)$.

Then $\mathbf{D}_n$ is an exotic drawing known as the *Heighway Dragon* of order $n$.  For example, $\mathbf{D}_{10}$ is shown below; counting each “F” as one step, the highlighted spot at $(18,16)$ is the position reached after $500$ steps.

![](../images/p220.gif)

What is the position of the cursor after $10^{12}$ steps in $D_{50}$ ?

Give your answer in the form $x,y$ with no spaces.


## 解决方案


## 代码


