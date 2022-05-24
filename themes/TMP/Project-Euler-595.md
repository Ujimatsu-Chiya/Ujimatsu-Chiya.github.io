---
title: Project Euler 595
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 595
## 题目
### Incremental Random Sort


A deck of cards numbered from 1 to n is shuffled randomly such that each permutation is equally likely.


The cards are to be sorted into ascending order using the following technique:
<ol><li> Look at the initial sequence of cards.  If it is already sorted, then there is no need for further action.  Otherwise, if any subsequences of cards happen to be in the correct place relative to one another (ascending with no gaps), then those subsequences are fixed by attaching the cards together.  For example, with 7 cards initially in the order 4123756, the cards labelled 1, 2 and 3 would be attached together, as would 5 and 6.
</li></ol><ol start="2"><li> The cards are 'shuffled' by being thrown into the air, but note that any correctly sequenced cards remain attached, so their orders are maintained.  The cards (or bundles of attached cards) are then picked up randomly.  You should assume that this randomisation is unbiased, despite the fact that some cards are single, and others are grouped together. 
</li></ol><ol start="3"><li> Repeat steps 1 and 2 until the cards are sorted. 
</li></ol>
   Let S(n) be the expected number of shuffles needed to sort the cards. Since the order is checked before the first shuffle, S(1) = 0. You are given that S(2) = 1, and S(5) = 4213/871.


Find S(52), and give your answer rounded to 8 decimal places.



# Project Euler 595
## 题目
### Incremental Random Sort

A deck of cards numbered from 1 to n is shuffled randomly such that each permutation is equally likely.
The cards are to be sorted into ascending order using the following technique:
<ol>
<li>Look at the initial sequence of cards.  If it is already sorted, then there is no need for further action.  Otherwise, if any subsequences of cards happen to be in the correct place relative to one another (ascending with no gaps), then those subsequences are fixed by attaching the cards together. For example, with 7 cards initially in the order 4123756, the cards labelled 1, 2 and 3 would be attached together, as would 5 and 6.</li>
<li>The cards are ‘shuffled’ by being thrown into the air, but note that any correctly sequenced cards remain attached, so their orders are maintained.  The cards (or bundles of attached cards) are then picked up randomly.  You should assume that this randomisation is unbiased, despite the fact that some cards are single, and others are grouped together. </li>
<li>Repeat steps 1 and 2 until the cards are sorted. </li>
</ol>
Let S(n) be the expected number of shuffles needed to sort the cards. Since the order is checked before the first shuffle, S(1) = 0. You are given that S(2) = 1, and S(5) = 4213/871.
Find S(52), and give your answer rounded to 8 decimal places.


## 解决方案


## 代码


