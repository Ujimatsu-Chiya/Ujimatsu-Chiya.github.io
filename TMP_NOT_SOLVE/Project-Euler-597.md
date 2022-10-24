---
title: Project Euler 597
category:
  - Project Euler
tags:
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 597
## 题目
### Torpids


The Torpids are rowing races held annually in Oxford, following some curious rules:

<ul><li>
A division consists of $n$ boats (typically 13), placed in order based on past performance.
</li><li>
All boats within a division start at 40 metre intervals along the river, in order with the highest-placed boat starting furthest upstream.
</li><li>
The boats all start rowing simultaneously, upstream, trying to catch the boat in front while avoiding being caught by boats behind.
</li><li>
Each boat continues rowing until <em>either</em> it reaches the finish line <em>or</em> it catches up with ("bumps") a boat in front.
</li><li>
The finish line is a distance $L$ metres (the course length, in reality about 1800 metres) upstream from the starting position of the lowest-placed boat. (Because of the staggered starting positions, higher-placed boats row a slightly shorter course than lower-placed boats.)
</li><li>
When a "bump" occurs, the "bumping" boat takes no further part in the race. The "bumped" boat must continue, however, and may even be "bumped" again by boats that started two or more places behind it.
</li><li>
After the race, boats are assigned new places within the division, based on the bumps that occurred. Specifically, for any boat $A$ that started in a lower place than $B$, then $A$ will be placed higher than $B$ in the new order if and only if one of the following occurred:
  <ol><li> $A$ bumped $B$ directly </li>
  <li> $A$ bumped another boat that went on to bump $B$ </li>
  <li> $A$ bumped another boat, that bumped yet another boat, that bumped $B$ </li>
  <li> etc </li></ol></li></ul><b>NOTE</b>: For the purposes of this problem you may disregard the boats' lengths, and assume that a bump occurs precisely when the two boats draw level. (In reality, a bump is awarded as soon as physical contact is made, which usually occurs when there is much less than a full boat length's overlap.)


Suppose that, in a particular race, each boat $B_j$ rows at a steady speed $v_j = -$log$X_j$ metres per second, where the $X_j$ are chosen randomly (with uniform distribution) between 0 and 1, independently from one another. These speeds are relative to the riverbank: you may disregard the flow of the river.


Let $p(n,L)$ be the probability that the new order is an <b>even permutation</b> of the starting order, when there are $n$ boats in the division and $L$ is the course length.


For example, with $n=3$ and $L=160$, labelling the boats as $A$,$B$,$C$ in starting order with $C$ highest, the different possible outcomes of the race are as follows:

<table cellspacing="15" align="center"><tr><th> Bumps occurring </th>
  <th> New order </th>
  <th> Permutation </th>
  <th> Probability </th>
 </tr><tr align="center"><td> none </td>
  <td> $A$, $B$, $C$ </td>
  <td> even </td>
  <td> $4/15$ </td>
 </tr><tr align="center"><td> $B$ bumps $C$ </td>
  <td> $A$, $C$, $B$ </td>
  <td> odd </td>
  <td> $8/45$ </td>
 </tr><tr align="center"><td> $A$ bumps $B$ </td>
  <td> $B$, $A$, $C$ </td>
  <td> odd </td>
  <td> $1/3$ </td>
 </tr><tr align="center"><td>     $B$ bumps $C$, then $A$ bumps $C$     </td>
  <td> $C$, $A$, $B$ </td>
  <td> even </td>
  <td> $4/27$ </td>
 </tr><tr align="center"><td>     $A$ bumps $B$, then $B$ bumps $C$     </td>
  <td> $C$, $B$, $A$ </td>
  <td> odd </td>
  <td> $2/27$ </td>
 </tr></table>
Therefore, $p(3,160) = 4/15 + 4/27 = 56/135$.


You are also given that $p(4,400)=0.5107843137$, rounded to 10 digits after the decimal point.


Find $p(13,1800)$ rounded to 10 digits after the decimal point.



# Project Euler 597
## 题目
### Torpids

The Torpids are rowing races held annually in Oxford, following some curious rules:
<ul>
<li>A division consists of $n$ boats (typically 13), placed in order based on past performance.</li>
<li>All boats within a division start at 40 metre intervals along the river, in order with the highest-placed boat starting furthest upstream.</li>
<li>The boats all start rowing simultaneously, upstream, trying to catch the boat in front while avoiding being caught by boats behind.</li>
<li>Each boat continues rowing until <i>either</i> it reaches the finish line <i>or</i> it catches up with (“bumps”) a boat in front.</li>
<li>The finish line is a distance $L$ metres (the course length, in reality about 1800 metres) upstream from the starting position of the lowest-placed boat. (Because of the staggered starting positions, higher-placed boats row a slightly shorter course than lower-placed boats.)</li>
<li>When a “bump” occurs, the “bumping” boat takes no further part in the race. The “bumped” boat must continue, however, and may even be “bumped” again by boats that started two or more places behind it.</li>
<li>After the race, boats are assigned new places within the division, based on the bumps that occurred. Specifically, for any boat $A$ that started in a lower place than $B$, then $A$ will be placed higher than $B$ in the new order if and only if one of the following occurred:<ol>
<li>$A$ bumped $B$ directly </li>
<li>$A$ bumped another boat that went on to bump $B$ </li>
<li>$A$ bumped another boat, that bumped yet another boat, that bumped $B$ </li>
<li>etc</li>
</ol>
</li>
</ul>
<b>NOTE</b>: For the purposes of this problem you may disregard the boats’ lengths, and assume that a bump occurs precisely when the two boats draw level. (In reality, a bump is awarded as soon as physical contact is made, which usually occurs when there is much less than a full boat length’s overlap.)
Suppose that, in a particular race, each boat $B_j$ rows at a steady speed $v_j = - \log X_j$ metres per second, where the $X_j$ are chosen randomly (with uniform distribution) between 0 and 1, independently from one another. These speeds are relative to the riverbank: you may disregard the flow of the river.
Let $p(n,L)$ be the probability that the new order is an <b>even permutation</b> of the starting order, when there are $n$ boats in the division and $L$ is the course length.
For example, with $n=3$ and $L=160$, labelling the boats as $A$,$B$,$C$ in starting order with $C$ highest, the different possible outcomes of the race are as follows:
<table>
<thead>
<tr>
<th align="center"><b>Bumps occurring</b></th>
<th align="center"><b>New order</b></th>
<th align="center"><b>Permutation</b></th>
<th align="center"><b>Probability</b></th>
</tr>
</thead>
<tbody><tr>
<td align="center">none</td>
<td align="center">$A$, $B$, $C$</td>
<td align="center">even</td>
<td align="center">4/15</td>
</tr>
<tr>
<td align="center">$B$ bumps $C$</td>
<td align="center">$A$, $C$, $B$</td>
<td align="center">odd</td>
<td align="center">8/45</td>
</tr>
<tr>
<td align="center">$A$ bumps $B$</td>
<td align="center">$B$, $A$, $C$</td>
<td align="center">odd</td>
<td align="center">1/3</td>
</tr>
<tr>
<td align="center">$B$ bumps $C$, then $A$ bumps $C$</td>
<td align="center">$C$, $A$, $B$</td>
<td align="center">even</td>
<td align="center">4/27</td>
</tr>
<tr>
<td align="center">$A$ bumps $B$, then $B$ bumps $C$</td>
<td align="center">$C$, $B$, $A$</td>
<td align="center">odd</td>
<td align="center">2/27</td>
</tr>
</tbody></table>
Therefore, $p(3,160) = 4/15 + 4/27 = 56/135$.
You are also given that $p(4,400)=0.5107843137$, rounded to 10 digits after the decimal point.
Find $p(13,1800)$ rounded to 10 digits after the decimal point.


## 解决方案


## 代码


