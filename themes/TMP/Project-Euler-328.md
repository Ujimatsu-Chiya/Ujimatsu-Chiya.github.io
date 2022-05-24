---
title: Project Euler 328
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 328
## 题目
### Lowest-cost Search

We are trying to find a hidden number selected from the set of integers {1, 2, \dots, <var>n</var>} by asking questions. 
Each number (question) we ask, has a <u>cost equal to the number asked</u> and we get one of three possible answers:<br /><ul><li> "Your guess is lower than the hidden number", or</li>
<li> "Yes, that's it!", or</li>
<li> "Your guess is higher than the hidden number".</li>
</ul>Given the value of <var>n</var>, an <i>optimal strategy</i> minimizes the total cost (i.e. the sum of all the questions asked) <u>for the worst possible case</u>. E.g.

If <var>n</var>=3, the best we can do is obviously to ask the number "<b>2</b>". The answer will immediately lead us to find the hidden number (at a total cost = 2).

If <var>n</var>=8, we might decide to use a "binary search" type of strategy: Our first question would be "<b>4</b>" and if the hidden number is higher than 4 we will need one or two additional questions.<br />
Let our second question be "<b>6</b>". If the hidden number is still higher than 6, we will need a third question in order to discriminate between 7 and 8.<br />
Thus, our third question will be "<b>7</b>" and the total cost for this worst-case scenario will be 4+6+7=<span style="color:#FF0000;"><b>17</b></span>.

We can improve considerably the worst-case cost for <var>n</var>=8, by asking "<b>5</b>" as our first question.<br />
If we are told that the hidden number is higher than 5, our second question will be "<b>7</b>", then we'll know for certain what the hidden number is (for a total cost of 5+7=<span style="color:#3333FF;"><b>12</b></span>).<br />
If we are told that the hidden number is lower than 5, our second question will be "<b>3</b>" and if the hidden number is lower than 3 our third question will be "<b>1</b>", giving a total cost of 5+3+1=<span style="color:#3333FF;"><b>9</b></span>.<br />
Since <span style="color:#3333FF;"><b>12</b></span>><span style="color:#3333FF;"><b>9</b></span>, the worst-case cost for this strategy is <span style="color:#FF0000;"><b>12</b></span>. That's better than what we achieved previously with the "binary search" strategy; it is also better than or equal to any other strategy.<br />
So, in fact, we have just described an optimal strategy for <var>n</var>=8.

Let C(<var>n</var>) be the worst-case cost achieved by an optimal strategy for <var>n</var>, as described above.<br />
Thus C(1) = 0, C(2) = 1, C(3) = 2 and C(8) = 12.<br />
Similarly, C(100) = 400 and $\sum \limits_{n = 1}^{100} {C(n)} = 17575$.

Find $\sum \limits_{n = 1}^{200000} {C(n)}$ .


# Project Euler 328
## 题目
### Lowest-cost Search

We are trying to find a hidden number selected from the set of integers {1, 2, \dots, n} by asking questions. Each number (question) we ask, has a <u>cost equal to the number asked</u> and we get one of three possible answers:
<ul>
<li>“Your guess is lower than the hidden number”, or</li>
<li>“Yes, that’s it!”, or</li>
<li>“Your guess is higher than the hidden number”.</li>
</ul>
Given the value of n, an <i>optimal strategy</i> minimizes the total cost (i.e. the sum of all the questions asked) <u>for the worst possible case</u>. E.g.
If n=3, the best we can do is obviously to ask the number “<b>2</b>“. The answer will immediately lead us to find the hidden number (at a total cost = 2).
If n=8, we might decide to use a “binary search” type of strategy: Our first question would be “<b>4</b>“ and if the hidden number is higher than 4 we will need one or two additional questions.<br>Let our second question be “<b>6</b>“. If the hidden number is still higher than 6, we will need a third question in order to discriminate between 7 and 8.<br>Thus, our third question will be “<b>7</b>“ and the total cost for this worst-case scenario will be 4+6+7=<span style="color:red;"><b>17</b></span>.
We can improve considerably the worst-case cost for n=8, by asking “<b>5</b>“ as our first question.<br>If we are told that the hidden number is higher than 5, our second question will be “<b>7</b>“, then we’ll know for certain what the hidden number is (for a total cost of 5+7=<span style="color:blue;"><b>12</b></span>).<br>If we are told that the hidden number is lower than 5, our second question will be “<b>3</b>“ and if the hidden number is lower than 3 our third question will be “<b>1</b>“, giving a total cost of 5+3+1=<span style="color:blue;"><b>9</b></span>.<br>Since <span style="color:blue;"><b>12</b></span>><span style="color:blue;"><b>9</b></span>, the worst-case cost for this strategy is <span style="color:red;"><b>12</b></span>. That’s better than what we achieved previously with the “binary search” strategy; it is also better than or equal to any other strategy.<br>So, in fact, we have just described an optimal strategy for n=8.
Let C(n) be the worst-case cost achieved by an optimal strategy for n, as described above.<br>Thus C(1) = 0, C(2) = 1, C(3) = 2 and C(8) = 12.<br>Similarly, C(100) = 400 and $\sum_{n=1}^{100}$C(n) = 17575.
Find $\sum_{n=1}^{200000}$C(n).


## 解决方案


## 代码


