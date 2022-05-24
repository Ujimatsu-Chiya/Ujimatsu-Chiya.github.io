---
title: Project Euler 566
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 566
## 题目
### Cake Icing Puzzle

Adam plays the following game with his birthday cake.

He cuts a piece forming a circular sector of 60 degrees and flips the piece upside down, with the icing on the bottom.<br />
He then rotates the cake by 60 degrees counterclockwise, cuts an adjacent 60 degree piece and flips it upside down.<br />
He keeps repeating this, until after a total of twelve steps, all the icing is back on top.

Amazingly, this works for any piece size, even if the cutting angle is an irrational number: all the icing will be back on top after a finite number of steps.

Now, Adam tries something different: he alternates cutting pieces of size $x=\frac{360}{9}$ degrees, $y=\frac{360}{10}$ degrees and $z=\frac{360 }{\sqrt{11}}$ degrees. The first piece he cuts has size <var>x</var> and he flips it. The second has size <var>y</var> and he flips it. The third has size <var>z</var> and he flips it. He repeats this with pieces of size <var>x</var>, <var>y</var> and <var>z</var> in that order until all the icing is back on top, and discovers he needs 60 flips altogether.

<div align="center"><img src="project/images/p566-cakeicingpuzzle.gif" alt="p566-cakeicingpuzzle.gif" /></div>

Let <var>F</var>(<var>a</var>, <var>b</var>, <var>c</var>) be the minimum number of piece flips needed to get all the icing back on top for pieces of size $x=\frac{360}{a}$ degrees, $y=\frac{360}{b}$ degrees and $z=\frac{360}{\sqrt{c}}$ degrees.<br />
Let $G(n) = \sum_{9 \le a < b < c \le n} F(a,b,c)$, for integers <var>a</var>, <var>b</var> and <var>c</var>.

You are given that <var>F</var>(9, 10, 11) = 60, <var>F</var>(10, 14, 16) = 506, <var>F</var>(15, 16, 17) = 785232.<br />
You are also given <var>G</var>(11) = 60, <var>G</var>(14) = 58020 and <var>G</var>(17) = 1269260.

Find <var>G</var>(53).


# Project Euler 566
## 题目
### Cake Icing Puzzle

Adam plays the following game with his birthday cake.
He cuts a piece forming a circular sector of 60 degrees and flips the piece upside down, with the icing on the bottom.<br>He then rotates the cake by 60 degrees counterclockwise, cuts an adjacent 60 degree piece and flips it upside down.<br>He keeps repeating this, until after a total of twelve steps, all the icing is back on top.
Amazingly, this works for any piece size, even if the cutting angle is an irrational number: all the icing will be back on top after a finite number of steps.
Now, Adam tries something different: he alternates cutting pieces of size $x=\frac{360}{9}$ degrees, $y=\frac{360}{10}$ degrees and $z=\frac{360}{\sqrt{11}}$ degrees. The first piece he cuts has size x and he flips it. The second has size y and he flips it. The third has size z and he flips it. He repeats this with pieces of size x, y and z in that order until all the icing is back on top, and discovers he needs 60 flips altogether.
<center><img src="https://projecteuler.net/project/images/p566-cakeicingpuzzle.gif" alt="p566-cakeicingpuzzle.gif"></center>

Let F(a, b, c) be the minimum number of piece flips needed to get all the icing back on top for pieces of size $x=\frac{360}{a}$ degrees, $y=\frac{360}{b}$ degrees and $z=\frac{360}{\sqrt{c}}$ degrees.<br>Let $G(n) = \sum_{9 \le a < b < c \le n} F(a,b,c)$, for integers a, b and c.
You are given that F(9,10,11)=60, F(10,14,16)=506, F(15,16,17)=785232.<br>You are also given G(11)=60, G(14)=58020 and G(17)=1269260.
Find G(53).


## 解决方案


## 代码


