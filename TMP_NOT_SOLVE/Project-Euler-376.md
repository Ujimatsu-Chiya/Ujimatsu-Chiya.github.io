---
title: Project Euler 376
category:
  - Project Euler
tags:
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 376
## 题目
### Nontransitive sets of dice



Consider the following set of dice with nonstandard pips:



Die A: 1 4 4 4 4 4<br />
Die B: 2 2 2 5 5 5<br />
Die C: 3 3 3 3 3 6<br />


A game is played by two players picking a die in turn and rolling it. The player who rolls the highest value wins.



If the first player picks die A and the second player picks die B we get<br />
P(second player wins) = ^7/_12 > ^1/_2


If the first player picks die B and the second player picks die C we get<br />
P(second player wins) = ^7/_12 > ^1/_2


If the first player picks die C and the second player picks die A we get<br />
P(second player wins) = ^25/_36 > ^1/_2


So whatever die the first player picks, the second player can pick another die and have a larger than 50% chance of winning.<br />
A set of dice having this property is called a <b>nontransitive set of dice</b>.



We wish to investigate how many sets of nontransitive dice exist. We will assume the following conditions:<ul><li>There are three six-sided dice with each side having between 1 and <var>N</var> pips, inclusive.</li>
<li>Dice with the same set of pips are equal, regardless of which side on the die the pips are located.</li>
<li>The same pip value may appear on multiple dice; if both players roll the same value neither player wins.</li>
<li>The sets of dice {A,B,C}, {B,C,A} and {C,A,B} are the same set.</li>
</ul>
For <var>N</var> = 7 we find there are 9780 such sets.<br />
How many are there for <var>N</var> = 30 ?



# Project Euler 376
## 题目
### Nontransitive sets of dice

Consider the following set of dice with nonstandard pips:
Die A: 1 4 4 4 4 4<br>Die B: 2 2 2 5 5 5<br>Die C: 3 3 3 3 3 6
A game is played by two players picking a die in turn and rolling it. The player who rolls the highest value wins.
If the first player picks die A and the second player picks die B we get<br>P(second player wins) = ^7/_12 > ^1/_2
If the first player picks die B and the second player picks die C we get<br>P(second player wins) = ^7/_12 > ^1/_2
If the first player picks die C and the second player picks die A we get<br>P(second player wins) = ^25/_36 > ^1/_2
So whatever die the first player picks, the second player can pick another die and have a larger than 50% chance of winning.<br>A set of dice having this property is called a <b>nontransitive set of dice</b>.
We wish to investigate how many sets of nontransitive dice exist. We will assume the following conditions:
<ul>
<li>There are three six-sided dice with each side having between 1 and N pips, inclusive.</li>
<li>Dice with the same set of pips are equal, regardless of which side on the die the pips are located.</li>
<li>The same pip value may appear on multiple dice; if both players roll the same value neither player wins.</li>
<li>The sets of dice {A,B,C}, {B,C,A} and {C,A,B} are the same set.</li>
</ul>
For N = 7 we find there are 9780 such sets.<br>How many are there for N = 30 ?


## 解决方案


## 代码


