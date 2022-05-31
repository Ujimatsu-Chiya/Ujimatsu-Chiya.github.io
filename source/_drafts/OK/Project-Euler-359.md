---
title: Project Euler 359
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 359
## 题目
### Hilbert's New Hotel



An infinite number of people (numbered 1, 2, 3, etc.) are lined up to get a room at Hilbert's newest infinite hotel. The hotel contains an infinite number of floors (numbered 1, 2, 3, etc.), and each floor contains an infinite number of rooms (numbered 1, 2, 3, etc.). 



Initially the hotel is empty. Hilbert declares a rule on how the <var>n</var>^th person is assigned a room: person <var>n</var> gets the first vacant room in the lowest numbered floor satisfying either of the following:
<ul>- the floor is empty
- the floor is not empty, and if the latest person taking a room in that floor is person <var>m</var>, then <var>m</var> + <var>n</var> is a perfect square
</ul>
Person 1 gets room 1 in floor 1 since floor 1 is empty.
<br />Person 2 does not get room 2 in floor 1 since 1 + 2 = 3 is not a perfect square.
<br />Person 2 instead gets room 1 in floor 2 since floor 2 is empty.
<br />Person 3 gets room 2 in floor 1 since 1 + 3 = 4 is a perfect square.



Eventually, every person in the line gets a room in the hotel.



Define P(<var>f</var>, <var>r</var>) to be <var>n</var> if person <var>n</var> occupies room <var>r</var> in floor <var>f</var>, and 0 if no person occupies the room. Here are a few examples:
<br />P(1, 1) = 1
<br />P(1, 2) = 3
<br />P(2, 1) = 2
<br />P(10, 20) = 440
<br />P(25, 75) = 4863
<br />P(99, 100) = 19454



Find the sum of all P(<var>f</var>, <var>r</var>) for all positive <var>f</var> and <var>r</var> such that <var>f</var> \times <var>r</var> = 71328803586048 and give the last 8 digits as your answer.



# Project Euler 359
## 题目
### Hilbert’s New Hotel

An infinite number of people (numbered $1, 2, 3,$ etc.) are lined up to get a room at Hilbert’s newest infinite hotel. The hotel contains an infinite number of floors (numbered $1, 2, 3,$ etc.), and each floor contains an infinite number of rooms (numbered $1, 2, 3,$ etc.). 

Initially the hotel is empty. Hilbert declares a rule on how the n^th person is assigned a room: person n gets the first vacant room in the lowest numbered floor satisfying either of the following:

- the floor is empty
- the floor is not empty, and if the latest person taking a room in that floor is person m, then m + n is a perfect square

Person $1$ gets room $1$ in floor $1$ since floor $1$ is empty.
Person $2$ does not get room $2$ in floor $1$ since $1 + 2 = 3$ is not a perfect square. Person $2$ instead gets room $1$ in floor $2$ since floor $2$ is empty. Person $3$ gets room $2$ in floor $1$ since $1 + 3 = 4$ is a perfect square.

Eventually, every person in the line gets a room in the hotel.

Define $P(f, r)$ to be $n$ if person $n$ occupies room $r$ in floor $f$, and $0$ if no person occupies the room. Here are a few examples:

$\begin{aligned}
&P(1, 1) = 1\\
&P(1, 2) = 3\\
&P(2, 1) = 2\\
&P(10, 20) = 440\\
&P(25, 75) = 4863\\
&P(99, 100) = 19454
\end{aligned}$


Find the sum of all $P(f, r)$ for all positive $f$ and $r$ such that $f \times r = 71328803586048$ and give the last $8$ digits as your answer.


## 解决方案


## 代码


