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

The quadtree encoding allows us to describe a $2^N\times 2^N$ black and white image as a sequence of bits (0 and 1). Those sequences are to be read from left to right like this:

- the first bit deals with the complete $2^N\times 2^N$ region;
“0” denotes a split:
- the current $2^n\times 2^n$ region is divided into 4 sub-regions of dimension $2^{n-1}\times 2^{n-1}$,
the next bits contains the description of the top left, top right, bottom left and bottom right sub-regions - in that order;
- “10” indicates that the current region contains only black pixels;
- “11” indicates that the current region contains only white pixels.
Consider the following $4\times 4$ image (colored marks denote places where a split can occur):

![](Project-Euler-287/p287_quadtree.gif)

This image can be described by several sequences, for example:
“<font color=red>0</font><font color=blue>0</font>10101010<font color=green>0</font>1011111011<font color=orange>0</font>10101010”, of length $30$, or
“<font color=red>0</font>10<font color=green>0</font>101111101110”, of length $16$, which is the minimal sequence for this image.

For a positive integer $N$, define $D_N$ as the $2^N\times 2^N$ image with the following coloring scheme:

- the pixel with coordinates $x = 0, y = 0$ corresponds to the bottom left pixel,
- if $(x-2^{N-1})^2 + (y-2^{N-1})^2 \leq 2^{2N-2}$ then the pixel is black,
- otherwise the pixel is white.

What is the length of the minimal sequence describing $D_{24}$ ?