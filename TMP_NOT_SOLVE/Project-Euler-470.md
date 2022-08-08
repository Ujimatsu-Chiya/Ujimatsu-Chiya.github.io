---
title: Project Euler 470
category:
  - Project Euler
tags:
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 470
## 题目
### Super Ramvok


Consider a single game of Ramvok:

Let <var>t</var> represent the maximum number of turns the game lasts. If <var>t</var> = 0, then the game ends immediately. Otherwise, on each turn <var>i</var>, the player rolls a die. After rolling, if <var>i</var> < <var>t</var> the player can either stop the game and receive a prize equal to the value of the current roll, or discard the roll and try again next turn. If <var>i</var> = <var>t</var>, then the roll cannot be discarded and the prize must be accepted. Before the game begins, <var>t</var> is chosen by the player, who must then pay an up-front cost <var>ct</var> for some constant <var>c</var>. For <var>c</var> = 0, <var>t</var> can be chosen to be infinite (with an up-front cost of 0). Let R(<var>d</var>, <var>c</var>) be the expected profit (i.e. net gain) that the player receives from a single game of optimally-played Ramvok, given a fair <var>d</var>-sided die and cost constant <var>c</var>. For example, R(4, 0.2) = 2.65. Assume that the player has sufficient funds for paying any/all up-front costs.

Now consider a game of Super Ramvok:

In Super Ramvok, the game of Ramvok is played repeatedly, but with a slight modification. After each game, the die is altered. The alteration process is as follows: The die is rolled once, and if the resulting face has its pips visible, then that face is altered to be blank instead. If the face is already blank, then it is changed back to its original value. After the alteration is made, another game of Ramvok can begin (and during such a game, at each turn, the die is rolled until a face with a value on it appears). The player knows which faces are blank and which are not at all times. The game of Super Ramvok ends once all faces of the die are blank.

Let S(<var>d</var>, <var>c</var>) be the expected profit that the player receives from an optimally-played game of Super Ramvok, given a fair <var>d</var>-sided die to start (with all sides visible), and cost constant <var>c</var>. For example, S(6, 1) = 208.3.

Let F(<var>n</var>) = <span style="font-size:larger;"><span style="font-size:larger;">\sum</span></span> _4\le<var>d</var>\le<var>n</var><span style="font-size:larger;"><span style="font-size:larger;">\sum</span></span> _0\le<var>c</var>\le<var>n</var> S(<var>d</var>, <var>c</var>).

Calculate F(20), rounded to the nearest integer.


# Project Euler 470
## 题目
### Super Ramvok

Consider a single game of Ramvok:
Let t represent the maximum number of turns the game lasts. If t = 0, then the game ends immediately. Otherwise, on each turn i, the player rolls a die. After rolling, if i < t the player can either stop the game and receive a prize equal to the value of the current roll, or discard the roll and try again next turn. If i = t, then the roll cannot be discarded and the prize must be accepted. Before the game begins, t is chosen by the player, who must then pay an up-front cost ct for some constant c. For c = 0, t can be chosen to be infinite (with an up-front cost of 0). Let R(d, c) be the expected profit (i.e. net gain) that the player receives from a single game of optimally-played Ramvok, given a fair d-sided die and cost constant c. For example, R(4, 0.2) = 2.65. Assume that the player has sufficient funds for paying any/all up-front costs.
Now consider a game of Super Ramvok:
In Super Ramvok, the game of Ramvok is played repeatedly, but with a slight modification. After each game, the die is altered. The alteration process is as follows: The die is rolled once, and if the resulting face has its pips visible, then that face is altered to be blank instead. If the face is already blank, then it is changed back to its original value. After the alteration is made, another game of Ramvok can begin (and during such a game, at each turn, the die is rolled until a face with a value on it appears). The player knows which faces are blank and which are not at all times. The game of Super Ramvok ends once all faces of the die are blank.
Let S(d, c) be the expected profit that the player receives from an optimally-played game of Super Ramvok, given a fair d-sided die to start (with all sides visible), and cost constant c. For example, S(6, 1) = 208.3.
Let F(n) = \sum_4\led\len \sum_0\lec\len S(d, c).
Calculate F(20), rounded to the nearest integer.


## 解决方案


## 代码


