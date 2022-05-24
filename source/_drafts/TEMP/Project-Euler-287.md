---
title: Project Euler 287
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 287
## 题目
### Quadtree encoding (a simple compression algorithm)

The quadtree encoding allows us to describe a 2^<var>N</var>\times2^<var>N</var>  black and white image as a sequence of bits (0 and 1). Those sequences are to be read from left to right like this:
<ul><li>the first bit deals with the complete 2^<var>N</var>\times2^<var>N</var> region;</li>
<li>"0" denotes a split:
<br />the current 2^<var>n</var>\times2^<var>n</var> region is divided into 4 sub-regions of dimension 2^<var>n</var>-1\times2^<var>n</var>-1,<br />
the next bits contains the description of the top left, top right, bottom left and bottom right sub-regions - in that order;</li>
<li>"10" indicates that the current region contains only black pixels;</li>
<li>"11" indicates that the current region contains only white pixels.</li></ul>Consider the following 4\times4 image (colored marks denote places where a split can occur):

<div class="center"><img src="project/images/p287_quadtree.gif" class="dark_img" alt="p287_quadtree.gif" /></div>

This image can be described by several sequences, for example :
"<span class="red strong">0</span><span class="blue strong">0</span>10101010<span class="green strong">0</span>1011111011<span class="orange strong">0</span>10101010", of length 30, or<br />
"<span class="red strong">0</span>10<span class="green strong"><b>0</b></span>101111101110", of length 16, which is the minimal sequence for this image.

For a positive integer <var>N</var>, define <var>D_N</var> as the 2^<var>N</var>\times2^<var>N</var> image with the following coloring scheme:
<ul><li>the pixel with coordinates <var>x</var> = 0, <var>y</var> = 0 corresponds to the bottom left pixel,</li>
<li>if (<var>x</var> - 2^<var>N</var>-1)^2 + (<var>y</var> - 2^<var>N</var>-1)^2 \le 2^2<var>N</var>-2 then the pixel is black,</li>
<li>otherwise the pixel is white.</li></ul>What is the length of the minimal sequence describing <var>D</var>_24 ?


# Project Euler 287
## 题目
### Quadtree encoding (a simple compression algorithm)

The quadtree encoding allows us to describe a 2^N\times2^N  black and white image as a sequence of bits (0 and 1). Those sequences are to be read from left to right like this:
<ul>
<li>the first bit deals with the complete 2^N\times2^N region;</li>
<li>“0” denotes a split:<br>the current 2^n\times2^n region is divided into 4 sub-regions of dimension 2^n-1\times2^n-1,<br>the next bits contains the description of the top left, top right, bottom left and bottom right sub-regions - in that order;</li>
<li>“10” indicates that the current region contains only black pixels;</li>
<li>“11” indicates that the current region contains only white pixels.</li>
</ul>
Consider the following 4\times4 image (colored marks denote places where a split can occur):
<center><img src="https://projecteuler.net/project/images/p287_quadtree.gif"></center>

This image can be described by several sequences, for example:<br>“<span style="color:red;"><b>0</b></span><span style="color:blue;"><b>0</b></span>10101010<span style="color:green;"><b>0</b></span>1011111011<span style="color:orange;"><b>0</b></span>10101010”, of length 30, or<br>“<span style="color:red;"><b>0</b></span>10<span style="color:green;"><b>0</b></span>101111101110”, of length 16, which is the minimal sequence for this image.
For a positive integer N, define D_N as the 2^N\times2^N image with the following coloring scheme:
<ul>
<li>the pixel with coordinates x&thinsp;=&thinsp;0, y&thinsp;=&thinsp;0 corresponds to the bottom left pixel,</li>
<li>if (x&thinsp;-&thinsp;2^N-1)^2&thinsp;+&thinsp;(y&thinsp;-&thinsp;2^N-1)^2&thinsp;\le&thinsp;2^2N-2 then the pixel is black,</li>
<li>otherwise the pixel is white.</li>
</ul>
What is the length of the minimal sequence describing D_24&thinsp;?


## 解决方案


## 代码


