---
title: Project Euler 472
category:
  - Project Euler
tags:
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 472
## 题目
### Comfortable Distance II


There are <var>N</var> seats in a row. <var>N</var> people come one after another to fill the seats according to the following rules:
<ol><li>No person sits beside another.</li>
<li>The first person chooses any seat.</li>
<li>Each subsequent person chooses the seat furthest from anyone else already seated, as long as it does not violate rule 1. If there is more than one choice satisfying this condition, then the person chooses the leftmost choice.</li>
</ol>Note that due to rule 1, some seats will surely be left unoccupied, and the maximum number of people that can be seated is less than <var>N</var> (for <var>N</var> > 1).

Here are the possible seating arrangements for <var>N</var> = 15:
<p align="center"><img src="project/images/p472_n15.png" class="dark_img" alt="p472_n15.png" />


We see that if the first person chooses correctly, the 15 seats can seat up to 7 people.<br />
We can also see that the first person has 9 choices to maximize the number of people that may be seated.

Let f(N) be the number of choices the first person has to maximize the number of occupants for <var>N</var> seats in a row. Thus, f(1) = 1, f(15) = 9, f(20) = 6, and f(500) = 16.

Also, <span style="font-size:larger;"><span style="font-size:larger;">\sum</span></span> f(N) = 83 for 1 \le <var>N</var> \le 20 and  <span style="font-size:larger;"><span style="font-size:larger;">\sum</span></span> f(N) = 13343 for 1 \le <var>N</var> \le 500.

Find <span style="font-size:larger;"><span style="font-size:larger;">\sum</span></span> f(N) for 1 \le <var>N</var> \le 10^12. Give the last 8 digits of your answer.



# Project Euler 472
## 题目
### Comfortable Distance II

There are N seats in a row. N people come one after another to fill the seats according to the following rules:
<ol>
<li>No person sits beside another.</li>
<li>The first person chooses any seat.</li>
<li>Each subsequent person chooses the seat furthest from anyone else already seated, as long as it does not violate rule 1. If there is more than one choice satisfying this condition, then the person chooses the leftmost choice.</li>
</ol>
Note that due to rule 1, some seats will surely be left unoccupied, and the maximum number of people that can be seated is less than N (for N > 1).
Here are the possible seating arrangements for N = 15:
<center><img src="https://projecteuler.net/project/images/p472_n15.png"></center>

We see that if the first person chooses correctly, the 15 seats can seat up to 7 people.<br>We can also see that the first person has 9 choices to maximize the number of people that may be seated.
Let f(N) be the number of choices the first person has to maximize the number of occupants for N seats in a row. Thus, f(1)&nbsp;=&nbsp;1, f(15)&nbsp;=&nbsp;9, f(20)&nbsp;=&nbsp;6, and f(500)&nbsp;=&nbsp;16.
Also, \sumf(N) = 83 for 1&nbsp;\le&nbsp;N&nbsp;\le&nbsp;20 and  \sumf(N) = 13343 for 1&nbsp;\le&nbsp;N&nbsp;\le&nbsp;500.
Find \sumf(N) for 1&nbsp;\le&nbsp;N&nbsp;\le&nbsp;10^12. Give the last 8 digits of your answer.


## 解决方案


## 代码


