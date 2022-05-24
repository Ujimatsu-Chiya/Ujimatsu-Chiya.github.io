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

Let <b><i>D</i></b>_0 be the two-letter string "Fa".  For n\ge1, derive <b><i>D</i></b>_n from <b><i>D</i></b>_n-1 by the string-rewriting rules:

<p style="margin-left:40px;">"a" → "aRbFR"<br />
"b" → "LFaLb"

Thus, <b><i>D</i></b>_0 = "Fa", <b><i>D</i></b>_1 = "FaRbFR", <b><i>D</i></b>_2 = "FaRbFRRLFaLbFR", and so on.

These strings can be interpreted as instructions to a computer graphics program, with "F" meaning "draw forward one unit", "L" meaning "turn left 90 degrees", "R" meaning "turn right 90 degrees", and "a" and "b" being ignored.  The initial position of the computer cursor is (0,0), pointing up towards (0,1).

Then <b><i>D</i></b>_n is an exotic drawing known as the <i>Heighway Dragon</i> of order <i>n</i>.  For example, <b><i>D</i></b>_10 is shown below; counting each "F" as one step, the highlighted spot at (18,16) is the position reached after 500 steps.

<div class="center">
<img src="project/images/p220.gif" class="dark_img" alt="" /></div>

What is the position of the cursor after 10^12 steps in <b><i>D</i></b>_50 ?<br />
Give your answer in the form <i>x</i>,<i>y</i> with no spaces.



# Project Euler 220
## 题目
### Heighway Dragon

Let <b>D</b>_0 be the two-letter string “Fa”. For n\ge1, derive <b>D</b>_n from <b>D</b>_n-1 by the string-rewriting rules:
“a” → “aRbFR”<br>“b” → “LFaLb”
Thus, <b>D</b>_0 = “Fa”, <b>D</b>_1 = “FaRbFR”, <b>D</b>_2 = “FaRbFRRLFaLbFR”, and so on.
These strings can be interpreted as instructions to a computer graphics program, with “F” meaning “draw forward one unit”, “L” meaning “turn left 90 degrees”, “R” meaning “turn right 90 degrees”, and “a” and “b” being ignored. The initial position of the computer cursor is (0,0), pointing up towards (0,1).
Then <b>D</b>_n is an exotic drawing known as the <i>Heighway Dragon</i> of order n.  For example, <b>D</b>_10 is shown below; counting each “F” as one step, the highlighted spot at (18,16) is the position reached after 500 steps.
<center><img src="https://projecteuler.net/project/images/p220.gif" alt=""></center>

What is the position of the cursor after 10^12 steps in <b>D</b>_50 ?<br>Give your answer in the form x,y with no spaces.


## 解决方案


## 代码


