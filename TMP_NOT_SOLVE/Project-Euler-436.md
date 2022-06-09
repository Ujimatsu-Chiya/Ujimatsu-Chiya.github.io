---
title: Project Euler 436
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 436
## 题目
### Unfair wager

Julie proposes the following wager to her sister Louise.<br />
She suggests they play a game of chance to determine who will wash the dishes.<br />
For this game, they shall use a generator of independent random numbers uniformly distributed between 0 and 1.<br />
The game starts with <var>S</var> = 0.<br />
The first player, Louise, adds to <var>S</var> different random numbers from the generator until <var>S</var> > 1 and records her last random number '<var>x</var>'.<br />
The second player, Julie, continues adding to <var>S</var> different random numbers from the generator until <var>S</var> > 2 and records her last random number '<var>y</var>'.<br />
The player with the highest number wins and the loser washes the dishes, i.e. if <var>y</var> > <var>x</var> the second player wins.

For example, if the first player draws 0.62 and 0.44, the first player turn ends since 0.62+0.44 > 1 and <var>x</var> = 0.44.<br />
If the second players draws 0.1, 0.27 and 0.91, the second player turn ends since 0.62+0.44+0.1+0.27+0.91 > 2 and <var>y</var> = 0.91.
Since <var>y</var> > <var>x</var>, the second player wins.

Louise thinks about it for a second, and objects: "That's not fair".<br />
What is the probability that the second player wins?<br />
Give your answer rounded to 10 places behind the decimal point in the form 0.abcdefghij



# Project Euler 436
## 题目
### Unfair wager

Julie proposes the following wager to her sister Louise.<br>She suggests they play a game of chance to determine who will wash the dishes.<br>For this game, they shall use a generator of independent random numbers uniformly distributed between 0 and 1.<br>The game starts with S = 0.<br>The first player, Louise, adds to S different random numbers from the generator until S > 1 and records her last random number ‘x’.<br>The second player, Julie, continues adding to S different random numbers from the generator until S > 2 and records her last random number ‘y’.<br>The player with the highest number wins and the loser washes the dishes, i.e. if y > x the second player wins.
For example, if the first player draws 0.62 and 0.44, the first player turn ends since 0.62+0.44 > 1 and x = 0.44.<br>If the second players draws 0.1, 0.27 and 0.91, the second player turn ends since 0.62+0.44+0.1+0.27+0.91 > 2 and y = 0.91.<br>Since y > x, the second player wins.
Louise thinks about it for a second, and objects: “That’s not fair”.<br>What is the probability that the second player wins?<br>Give your answer rounded to 10 places behind the decimal point in the form 0.abcdefghij


## 解决方案


## 代码


