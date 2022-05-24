---
title: Project Euler 589
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 589
## 题目
### Poohsticks Marathon


Christopher Robin and Pooh Bear love the game of Poohsticks so much that they invented a new version which allows them to play for longer before one of them wins and they have to go home for tea. The game starts as normal with both dropping a stick simultaneously on the upstream side of a bridge. But rather than the game ending when one of the sticks emerges on the downstream side, instead they fish their sticks out of the water, and drop them back in again on the upstream side. The game only ends when one of the sticks emerges from under the bridge ahead of the other one having also 'lapped' the other stick - that is, having made one additional journey under the bridge compared to the other stick.


On a particular day when playing this game, the time taken for a stick to travel under the bridge varies between a minimum of 30 seconds, and a maximum of 60 seconds. The time taken to fish a stick out of the water and drop it back in again on the other side is 5 seconds. The current under the bridge has the unusual property that the sticks' journey time is always an integral number of seconds, and it is equally likely to emerge at any of the possible times between 30 and 60 seconds (inclusive). It turns out that under these circumstances, the expected time for playing a single game is 1036.15 seconds (rounded to 2 decimal places). This time is measured from the point of dropping the sticks for the first time, to the point where the winning stick emerges from under the bridge having lapped the other.


The stream flows at different rates each day, but maintains the property that the journey time in seconds is equally distributed amongst the integers from a minimum, $n$, to a maximum, $m$, inclusive. Let the expected time of play in seconds be $E(m,n)$. Hence $E(60,30)=1036.15\dots$


Let $S(k)=\sum_{m=2}^k\sum_{n=1}^{m-1}E(m,n)$.


For example $S(5)=7722.82$ rounded to 2 decimal places.


Find $S(100)$ and give your answer rounded to 2 decimal places.



# Project Euler 589
## 题目
### Poohsticks Marathon

Christopher Robin and Pooh Bear love the game of Poohsticks so much that they invented a new version which allows them to play for longer before one of them wins and they have to go home for tea. The game starts as normal with both dropping a stick simultaneously on the upstream side of a bridge. But rather than the game ending when one of the sticks emerges on the downstream side, instead they fish their sticks out of the water, and drop them back in again on the upstream side. The game only ends when one of the sticks emerges from under the bridge ahead of the other one having also ‘lapped’ the other stick - that is, having made one additional journey under the bridge compared to the other stick.
On a particular day when playing this game, the time taken for a stick to travel under the bridge varies between a minimum of 30 seconds, and a maximum of 60 seconds. The time taken to fish a stick out of the water and drop it back in again on the other side is 5 seconds. The current under the bridge has the unusual property that the sticks’ journey time is always an integral number of seconds, and it is equally likely to emerge at any of the possible times between 30 and 60 seconds (inclusive). It turns out that under these circumstances, the expected time for playing a single game is 1036.15 seconds (rounded to 2 decimal places). This time is measured from the point of dropping the sticks for the first time, to the point where the winning stick emerges from under the bridge having lapped the other.
The stream flows at different rates each day, but maintains the property that the journey time in seconds is equally distributed amongst the integers from a minimum, $n$, to a maximum, $m$, inclusive. Let the expected time of play in seconds be $E(m,n)$. Hence $E(60,30)=1036.15\dots$
Let $S(k)=\sum_{m=2}^k\sum_{n=1}^{m-1}E(m,n)$.
For example $S(5)=7722.82$ rounded to 2 decimal places.
Find $S(100)$ and give your answer rounded to 2 decimal places.


## 解决方案


## 代码


