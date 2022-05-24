---
title: Project Euler 244
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 244
## 题目
### Sliders

You probably know the game <i>Fifteen Puzzle</i>. Here, instead of numbered tiles, we have seven red tiles and eight blue tiles.
A move is denoted by the uppercase initial of the direction (Left, Right, Up, Down) in which the tile is slid, e.g. starting from configuration (<b>S</b>), by the sequence <b>LULUR</b> we reach the configuration (<b>E</b>):
<div class="center">
<table cellspacing="0" cellpadding="2" border="0" align="center"><tr><td width="25">(<b>S</b>)</td><td width="100"><img src="project/images/p244_start.gif" class="dark_img" alt="p244_start.gif" /></td><td width="25">, (<b>E</b>)</td><td width="100"><img src="project/images/p244_example.gif" class="dark_img" alt="p244_example.gif" /></td>
</tr></table></div>

For each path, its checksum is calculated by (pseudocode):
<div style="margin-left:100px;">
checksum = 0<br />
checksum = (checksum \times 243 + <var>m</var>_1) mod 100 000 007<br />
checksum = (checksum \times 243 + <var>m</var>_2) mod 100 000 007<br />
   \dots<br />
checksum = (checksum \times 243 + <var>m</var>_<var>n</var>) mod 100 000 007<br /></div>
where <var>m</var>_<var>k</var> is the ASCII value of the <var>k</var>^<var>th</var> letter in the move sequence and the ASCII values for the moves are:

<div class="center">
<table cellspacing="0" cellpadding="2" border="1" align="center"><tr><td width="30"><b>L</b></td><td width="30">76</td></tr><tr><td><b>R</b></td><td>82</td></tr><tr><td><b>U</b></td><td>85</td></tr><tr><td><b>D</b></td><td>68</td></tr></table></div>

For the sequence <b>LULUR</b> given above, the checksum would be 19761398.
Now, starting from configuration (<b>S</b>),
find all shortest ways to reach configuration (<b>T</b>).
<div class="center">
<table cellspacing="0" cellpadding="2" border="0" align="center"><tr><td width="25">(<b>S</b>)</td><td width="100"><img src="project/images/p244_start.gif" class="dark_img" alt="p244_start.gif" /></td><td width="25">, (<b>T</b>)</td><td width="100"><img src="project/images/p244_target.gif" class="dark_img" alt="p244_target.gif" /></td>
</tr></table></div>

What is the sum of all checksums for the paths having the minimal length?


# Project Euler 244
## 题目
### Sliders

You probably know the game <i>Fifteen Puzzle</i>. Here, instead of numbered tiles, we have seven red tiles and eight blue tiles.
A move is denoted by the uppercase initial of the direction (Left, Right, Up, Down) in which the tile is slid, e.g. starting from configuration (<b>S</b>), by the sequence <b>LULUR</b> we reach the configuration (<b>E</b>):
<center><img src="https://projecteuler.net/project/images/p244_start.gif"></center>
<center>(S)</center>
<center><img src="https://projecteuler.net/project/images/p244_example.gif"></center>
<center>(E)</center>

For each path, its checksum is calculated by (pseudocode):
<blockquote>
checksum = 0<br>checksum = (checksum \times 243 + m_1) mod 100&thinsp;000&thinsp;007<br>checksum = (checksum \times 243 + m_2) mod 100&thinsp;000&thinsp;007<br>&nbsp;&nbsp;&nbsp;\dots<br>checksum = (checksum \times 243 + m_n) mod 100&thinsp;000&thinsp;007
</blockquote>
where m_k is the ASCII value of the k^th letter in the move sequence and the ASCII values for the moves are:
<table>
<thead>
<tr>
<th align="center">&nbsp;</th>
<th align="center">&nbsp;</th>
</tr>
</thead>
<tbody><tr>
<td align="center">L</td>
<td align="center">76</td>
</tr>
<tr>
<td align="center">R</td>
<td align="center">82</td>
</tr>
<tr>
<td align="center">U</td>
<td align="center">85</td>
</tr>
<tr>
<td align="center">D</td>
<td align="center">68</td>
</tr>
</tbody></table>
For the sequence <b>LULUR</b> given above, the checksum would be 19761398.
Now, starting from configuration (<b>S</b>), find all shortest ways to reach configuration (<b>T</b>).
<center><img src="https://projecteuler.net/project/images/p244_start.gif"></center>
<center>(S)</center>
<center><img src="https://projecteuler.net/project/images/p244_target.gif"></center>
<center>(T)</center>

What is the sum of all checksums for the paths having the minimal length?


## 解决方案


## 代码


