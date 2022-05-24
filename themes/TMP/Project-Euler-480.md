---
title: Project Euler 480
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 480
## 题目
### The Last Question

Consider all the words which can be formed by selecting letters, in any order, from the phrase:
<div class="center"><b>thereisasyetinsufficientdataforameaningfulanswer</b></div>
Suppose those with 15 letters or less are listed in <b>alphabetical order</b> and numbered sequentially starting at 1.<br />
The list would include:
<ul style="list-style-type:none;"><li>1 : a</li>
<li>2 : aa</li>
<li>3 : aaa</li>
<li>4 : aaaa</li>
<li>5 : aaaaa</li>
<li>6 : aaaaaa</li>
<li>7 : aaaaaac</li>
<li>8 : aaaaaacd</li>
<li>9 : aaaaaacde</li>
<li>10 : aaaaaacdee</li>
<li>11 : aaaaaacdeee</li>
<li>12 : aaaaaacdeeee</li>
<li>13 : aaaaaacdeeeee</li>
<li>14 : aaaaaacdeeeeee</li>
<li>15 : aaaaaacdeeeeeef</li>
<li>16 : aaaaaacdeeeeeeg</li>
<li>17 : aaaaaacdeeeeeeh</li>
<li>\dots</li>
<li>28 : aaaaaacdeeeeeey</li>
<li>29 : aaaaaacdeeeeef</li>
<li>30 : aaaaaacdeeeeefe</li>
<li>\dots</li>
<li>115246685191495242: euleoywuttttsss</li>
<li>115246685191495243: euler</li>
<li>115246685191495244: eulera</li>
<li>\dots</li>
<li>525069350231428029: ywuuttttssssrrr</li></ul>Define <var>P</var>(<var>w</var>) as the position of the word <var>w</var>.<br />
Define <var>W</var>(<var>p</var>) as the word in position <var>p</var>.<br />
We can see that <var>P</var>(<var>w</var>) and <var>W</var>(<var>p</var>) are inverses: <var>P</var>(<var>W</var>(<var>p</var>)) = <var>p</var> and <var>W</var>(<var>P</var>(<var>w</var>)) = <var>w</var>.
Examples:
<ul style="list-style-type:none;"><li><var>W</var>(10) = aaaaaacdee</li>
<li><var>P</var>(aaaaaacdee) = 10</li>
<li><var>W</var>(115246685191495243) = euler</li>
<li><var>P</var>(euler) = 115246685191495243</li></ul>Find <var>W</var>(<var>P</var>(legionary) + <var>P</var>(calorimeters) - <var>P</var>(annihilate) + <var>P</var>(orchestrated) - <var>P</var>(fluttering)).<br />
Give your answer using lowercase characters (no punctuation or space).



# Project Euler 480
## 题目
### The Last Question

Consider all the words which can be formed by selecting letters, in any order, from the phrase:
<center>**thereisasyetinsufficientdataforameaningfulanswer**</center>

Suppose those with 15 letters or less are listed in **alphabetical order** and numbered sequentially starting at 1.<br>The list would include:
1 : a<br>2 : aa<br>3 : aaa<br>4 : aaaa<br>5 : aaaaa<br>6 : aaaaaa<br>7 : aaaaaac<br>8 : aaaaaacd<br>9 : aaaaaacde<br>10 : aaaaaacdee<br>11 : aaaaaacdeee<br>12 : aaaaaacdeeee<br>13 : aaaaaacdeeeee<br>14 : aaaaaacdeeeeee<br>15 : aaaaaacdeeeeeef<br>16 : aaaaaacdeeeeeeg<br>17 : aaaaaacdeeeeeeh<br>\dots<br>28 : aaaaaacdeeeeeey<br>29 : aaaaaacdeeeeef<br>30 : aaaaaacdeeeeefe<br>\dots<br>115246685191495242: euleoywuttttsss<br>115246685191495243: euler<br>115246685191495244: eulera<br>\dots<br>525069350231428029: ywuuttttssssrrr
Define P(w) as the position of the word w.<br>Define W(p) as the word in position p.<br>We can see that P(w) and W(p) are inverses: P(W(p)) = p and W(P(w)) = w.
Examples:
W(10) = aaaaaacdee<br>P(aaaaaacdee) = 10<br>W(115246685191495243) = euler<br>P(euler) = 115246685191495243
Find W(P(legionary) + P(calorimeters) - P(annihilate) + P(orchestrated) - P(fluttering)).<br>Give your answer using lowercase characters (no punctuation or space).


## 解决方案


## 代码


