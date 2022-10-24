---
title: Project Euler 298
category:
  - Project Euler
tags:
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 298
## 题目
### Selective Amnesia


Larry and Robin play a memory game involving a sequence of random numbers between 1 and 10, inclusive, that are called out one at a time. Each player can remember up to 5 previous numbers. When the called number is in a player's memory, that player is awarded a point. If it's not, the player adds the called number to his memory, removing another number if his memory is full.

Both players start with empty memories. Both players always add new missed numbers to their memory but use a different strategy in deciding which number to remove:<br />
Larry's strategy is to remove the number that hasn't been called in the longest time.<br />
Robin's strategy is to remove the number that's been in the memory the longest time.

Example game:
<table class="grid center"><tr><th>Turn</th>
  <th>Called<br />number</th>
  <th class="right">Larry's<br />memory</th>
  <th>Larry's<br />score</th>
  <th class="right">Robin's<br />memory</th>
  <th>Robin's<br />score</th>
</tr><tr><td>1</td>
  <td>1</td>
  <td class="right">1</td>
  <td>0</td>
  <td class="right">1</td>
  <td>0</td>
</tr><tr><td>2</td>
  <td>2</td>
  <td class="right">1,2</td>
  <td>0</td>
  <td class="right">1,2</td>
  <td>0</td>
</tr><tr><td>3</td>
  <td>4</td>
  <td class="right">1,2,4</td>
  <td>0</td>
  <td class="right">1,2,4</td>
  <td>0</td>
</tr><tr><td>4</td>
  <td>6</td>
  <td class="right">1,2,4,6</td>
  <td>0</td>
  <td class="right">1,2,4,6</td>
  <td>0</td>
</tr><tr><td>5</td>
  <td>1</td>
  <td class="right">1,2,4,6</td>
  <td>1</td>
  <td class="right">1,2,4,6</td>
  <td>1</td>
</tr><tr><td>6</td>
  <td>8</td>
  <td class="right">1,2,4,6,8</td>
  <td>1</td>
  <td class="right">1,2,4,6,8</td>
  <td>1</td>
</tr><tr><td>7</td>
  <td>10</td>
  <td class="right">1,4,6,8,10</td>
  <td>1</td>
  <td class="right">2,4,6,8,10</td>
  <td>1</td>
</tr><tr><td>8</td>
  <td>2</td>
  <td class="right">1,2,6,8,10</td>
  <td>1</td>
  <td class="right">2,4,6,8,10</td>
  <td>2</td>
</tr><tr><td>9</td>
  <td>4</td>
  <td class="right">1,2,4,8,10</td>
  <td>1</td>
  <td class="right">2,4,6,8,10</td>
  <td>3</td>
</tr><tr><td>10</td>
  <td>1</td>
  <td class="right">1,2,4,8,10</td>
  <td>2</td>
  <td class="right">1,4,6,8,10</td>
  <td>3</td>
</tr></table>Denoting Larry's score by <var>L</var> and Robin's score by <var>R</var>, what is the expected value of |<var>L</var>-<var>R</var>| after 50 turns? Give your answer rounded to eight decimal places using the format x.xxxxxxxx .


# Project Euler 298
## 题目
### Selective Amnesia

Larry and Robin play a memory game involving of a sequence of random numbers between 1 and 10, inclusive, that are called out one at a time. Each player can remember up to 5 previous numbers. When the called number is in a player’s memory, that player is awarded a point. If it’s not, the player adds the called number to his memory, removing another number if his memory is full.
Both players start with empty memories. Both players always add new missed numbers to their memory but use a different strategy in deciding which number to remove:<br>Larry’s strategy is to remove the number that hasn’t been called in the longest time.<br>Robin’s strategy is to remove the number that’s been in the memory the longest time.
Example game:
<table>
<thead>
<tr>
<th align="center">Turn</th>
<th align="center">Called number</th>
<th align="center">Larry’s memory</th>
<th align="center">Larry’s score</th>
<th align="center">Robin’s memory</th>
<th align="center">Robin’s score</th>
</tr>
</thead>
<tbody><tr>
<td align="center">1</td>
<td align="center">1</td>
<td align="center">1</td>
<td align="center">0</td>
<td align="center">1</td>
<td align="center">0</td>
</tr>
<tr>
<td align="center">2</td>
<td align="center">2</td>
<td align="center">1,2</td>
<td align="center">0</td>
<td align="center">1,2</td>
<td align="center">0</td>
</tr>
<tr>
<td align="center">3</td>
<td align="center">4</td>
<td align="center">1,2,4</td>
<td align="center">0</td>
<td align="center">1,2,4</td>
<td align="center">0</td>
</tr>
<tr>
<td align="center">4</td>
<td align="center">6</td>
<td align="center">1,2,4,6</td>
<td align="center">0</td>
<td align="center">1,2,4,6</td>
<td align="center">0</td>
</tr>
<tr>
<td align="center">5</td>
<td align="center">1</td>
<td align="center">1,2,4,6</td>
<td align="center">1</td>
<td align="center">1,2,4,6</td>
<td align="center">1</td>
</tr>
<tr>
<td align="center">6</td>
<td align="center">8</td>
<td align="center">1,2,4,6,8</td>
<td align="center">1</td>
<td align="center">1,2,4,6,8</td>
<td align="center">1</td>
</tr>
<tr>
<td align="center">7</td>
<td align="center">10</td>
<td align="center">1,4,6,8,10</td>
<td align="center">1</td>
<td align="center">2,4,6,8,10</td>
<td align="center">1</td>
</tr>
<tr>
<td align="center">8</td>
<td align="center">2</td>
<td align="center">1,2,6,8,10</td>
<td align="center">1</td>
<td align="center">2,4,6,8,10</td>
<td align="center">2</td>
</tr>
<tr>
<td align="center">9</td>
<td align="center">4</td>
<td align="center">1,2,4,8,10</td>
<td align="center">1</td>
<td align="center">2,4,6,8,10</td>
<td align="center">3</td>
</tr>
<tr>
<td align="center">10</td>
<td align="center">1</td>
<td align="center">1,2,4,8,10</td>
<td align="center">2</td>
<td align="center">1,4,6,8,10</td>
<td align="center">3</td>
</tr>
</tbody></table>
Denoting Larry’s score by L and Robin’s score by R, what is the expected value of |L-R| after 50 turns? Give your answer rounded to eight decimal places using the format x.xxxxxxxx.


## 解决方案


## 代码


