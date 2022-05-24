---
title: Project Euler 406
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 406
## 题目
### Guessing Game

We are trying to find a hidden number selected from the set of integers {1, 2, \dots, <var>n</var>} by asking questions. 
Each number (question) we ask, we get one of three possible answers:<br /><ul><li> "Your guess is lower than the hidden number" (and you incur a cost of <var>a</var>), or</li>
<li> "Your guess is higher than the hidden number" (and you incur a cost of <var>b</var>), or</li>
<li> "Yes, that's it!" (and the game ends).</li>
</ul>Given the value of <var>n</var>, <var>a</var>, and <var>b</var>, an <i>optimal strategy</i> minimizes the total cost <u>for the worst possible case</u>.

For example, if <var>n</var> = 5, <var>a</var> = 2, and <var>b</var> = 3, then we may begin by asking "<b>2</b>" as our first question.

If we are told that 2 is higher than the hidden number (for a cost of <var>b</var>=3), then we are sure that "<b>1</b>" is the hidden number (for a total cost of <span style="color:#3333ff;"><b>3</b></span>).<br />
If we are told that 2 is lower than the hidden number (for a cost of <var>a</var>=2), then our next question will be "<b>4</b>".<br />
If we are told that 4 is higher than the hidden number (for a cost of <var>b</var>=3), then we are sure that "<b>3</b>" is the hidden number (for a total cost of 2+3=<span style="color:#3333ff;"><b>5</b></span>).<br />
If we are told that 4 is lower than the hidden number (for a cost of <var>a</var>=2), then we are sure that "<b>5</b>" is the hidden number (for a total cost of 2+2=<span style="color:#3333ff;"><b>4</b></span>).<br />
Thus, the worst-case cost achieved by this strategy is <span style="color:#FF0000;"><b>5</b></span>. It can also be shown that this is the lowest worst-case cost that can be achieved. 
So, in fact, we have just described an optimal strategy for the given values of <var>n</var>, <var>a</var>, and <var>b</var>.

Let $C(n, a, b)$ be the worst-case cost achieved by an optimal strategy for the given values of <var>n</var>, <var>a</var> and <var>b</var>.

Here are a few examples:<br />
$C(5, 2, 3) = 5$<br />
$C(500, \sqrt 2, \sqrt 3) = 13.22073197\dots$<br />
$C(20000, 5, 7) = 82$<br />
$C(2000000, \sqrt 5, \sqrt 7) = 49.63755955\dots$

Let $F_k$ be the Fibonacci numbers: $F_k=F_{k-1}+F_{k-2}$ with base cases $F_1=F_2= 1$.<br />Find $\displaystyle \sum \limits_{k = 1}^{30} {C \left (10^{12}, \sqrt{k}, \sqrt{F_k} \right )}$, and give your answer rounded to 8 decimal places behind the decimal point.


# Project Euler 406
## 题目
### Guessing Game

We are trying to find a hidden number selected from the set of integers {1, 2, \dots, n} by asking questions. Each number (question) we ask, we get one of three possible answers:
<ul>
<li>“Your guess is lower than the hidden number” (and you incur a cost of a), or</li>
<li>“Your guess is higher than the hidden number” (and you incur a cost of b), or</li>
<li>“Yes, that’s it!” (and the game ends).</li>
</ul>
Given the value of n, a, and b, an <em>optimal strategy</em> minimizes the total cost <u>for the worst possible case</u>.
For example, if n = 5, a = 2, and b = 3, then we may begin by asking “**2**“ as our first question.
If we are told that 2 is higher than the hidden number (for a cost of b=3), then we are sure that “**1**“ is the hidden number (for a total cost of <span style="color:blue;">**3**</span>).<br>If we are told that 2 is lower than the hidden number (for a cost of a=2), then our next question will be “**4**“.<br>If we are told that 4 is higher than the hidden number (for a cost of b=3), then we are sure that “**3**“ is the hidden number (for a total cost of 2+3=<span style="color:blue;">**5**</span>).<br>If we are told that 4 is lower than the hidden number (for a cost of a=2), then we are sure that “**5**“ is the hidden number (for a total cost of 2+2=<span style="color:blue;">**4**</span>).<br>Thus, the worst-case cost achieved by this strategy is <span style="color:red;">**5**</span>. It can also be shown that this is the lowest worst-case cost that can be achieved. So, in fact, we have just described an optimal strategy for the given values of n, a, and b.
Let C(n, a, b) be the worst-case cost achieved by an optimal strategy for the given values of n, a, and b.
Here are a few examples:<br>C(5, 2, 3) = 5<br>C(500, √2, √3) = 13.22073197\dots<br>C(20000, 5, 7) = 82<br>C(2000000, √5, √7) = 49.63755955\dots
Let F_k be the Fibonacci numbers: F_k = F_k-1 + F_k-2 with base cases F_1 = F_2 = 1.<br>Find \sum_1\lek\le30&nbsp;C(10^12, √k, √F_k), and give your answer rounded to 8 decimal places behind the decimal point.


## 解决方案


## 代码


