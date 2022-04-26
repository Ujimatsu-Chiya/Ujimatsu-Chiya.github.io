---
title: Project Euler 89
tags:
  - Project Euler
mathjax: true
date: 2022-04-26 16:10:19
---

<escape><!-- more --></escape>

# Project Euler 89
## 题目
### Roman numerals
For a number written in Roman numerals to be considered valid there are basic rules which must be followed. Even though the rules allow some numbers to be expressed in more than one way there is always a “best” way of writing a particular number.
For example, it would appear that there are at least six ways of writing the number sixteen:

<span style="font-family:courier new,monospace;">IIIIIIIIIIIIIIII</span> </br><span style="font-family:courier new,monospace;">VIIIIIIIIIII</span> </br><span style="font-family:courier new,monospace;">VVIIIIII</span> </br><span style="font-family:courier new,monospace;">XIIIIII</span></br><span style="font-family:courier new,monospace;">VVVI</span> </br><span style="font-family:courier new,monospace;">XVI</span></br>

However, according to the rules only <span style="font-family:courier new,monospace;">XIIIIII</span> and <span style="font-family:courier new,monospace;">XVI</span> are valid, and the last example is considered to be the most efficient, as it uses the least number of numerals.

The 11K text file, [roman.txt](./resources/p089_roman.txt) (right click and ‘Save Link/Target As…’), contains one thousand numbers written in valid, but not necessarily minimal, Roman numerals; see <a href="https://projecteuler.net/about=roman_numerals" target="_blank" rel="noopener">About… Roman Numerals</a> for the definitive rules for this problem.

Find the number of characters saved by writing each of these in their minimal form.
Note: You can assume that all the Roman numerals in the file contain no more than four consecutive identical units.