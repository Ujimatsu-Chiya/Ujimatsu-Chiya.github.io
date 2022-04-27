---
title: Project Euler 159
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 159
## 题目
### Digital root sums of factorisations

A composite number can be factored many different ways.  
For instance, not including multiplication by one, 24 can be factored in 7 distinct ways:
<div class="margin_left">
24 = 2x2x2x3<br />
24 = 2x3x4<br />
24 = 2x2x6<br />
24 = 4x6<br />
24 = 3x8<br />
24 = 2x12<br />
24 = 24


# Project Euler 159
## 题目
### YPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=2">
<meta name="theme-color" content="#222">
<meta name="generator" content="Hexo 4.2.1">
  <link rel="icon" type="image/png" sizes="32x32" href="/images/32x32.png">
  <link rel="icon" type="image/png" sizes="16x16" href="/images/16x16.png">

<link rel="stylesheet" href="/css/main.css">

<link rel="stylesheet" href="//fonts.googleapis.com/css?family=Lato:300,300italic,400,400italic,700,700italic|Lato', 'Microsoft Yahei Light:300,300italic,400,400italic,700,700italic|Cambria', 'Microsoft Yahei Light:300,300italic,400,400italic,700,700italic|Verdana', Lato, 'Microsoft Yahei Light:300,300italic,400,400italic,700,700italic&display=swap&subset=latin,latin-ext">
<link rel="stylesheet" href="/lib/font-awesome/css/all.min.css">

<script id="hexo-configurations">
    var NexT = window.NexT || {};
    var CONFIG = {"hostname":"yoursite.com","root":"/","scheme":"Mist","version":"7.8.0","exturl":false,"sidebar":{"position":"right","display":"hide","padding":18,"offset":12,"onmobile":false},"copycode":{"enable":false,"show_result":false,"style":null},"back2top":{"enable":true,"sidebar":false,"scrollpercent":false},"bookmark":{"enable":false,"color":"#222","save":"auto"},"fancybox":false,"mediumzoom":false,"lazyload":false,"pangu":false,"comments":{"style":"tabs","active":null,"storage":true,"lazyload":false,"nav":null},"algolia":{"hits":{"per_page":10},"labels":{"input_placeholder":"Search for Posts","hits_empty":"We didn't find any results for the search: ${query}","hits_stats":"${hits} results found in ${time} ms"}},"localsearch":{"enable":true,"trigger":"auto","top_n_per_article":1,"unescape":false,"preload":false},"motion":{"enable":true,"async":false,"transition":{"post_block":"fadeIn","post_header":"slideDownIn","post_body":"slideDownIn","coll_header":"slideLeftIn","sidebar":"slideUpIn"}},"path":"search.xml"};
  
<b>Digital root sums of factorisations</b>
A composite number can be factored many different ways. For instance, not including multiplication by one, 24 can be factored in 7 distinct ways:
24 = 2x2x2x3<br>24 = 2x3x4<br>24 = 2x2x6<br>24 = 4x6<br>24 = 3x8<br>24 = 2x12<br>24 = 24
Recall that the digital root of a number, in base 10, is found by adding together the digits of that number, and repeating that process until a number is arrived at that is less than 10. Thus the digital root of 467 is 8.
We shall call a Digital Root Sum (DRS) the sum of the digital roots of the individual factors of our number.<br>The chart below demonstrates all of the DRS values for 24.
<table>
<thead>
<tr>
<th align="center">Factorisation</th>
<th align="center">Digital Root Sum</th>
</tr>
</thead>
<tbody><tr>
<td align="center">2x2x2x3</td>
<td align="center">9</td>
</tr>
<tr>
<td align="center">2x3x4</td>
<td align="center">9</td>
</tr>
<tr>
<td align="center">2x2x6</td>
<td align="center">10</td>
</tr>
<tr>
<td align="center">4x6</td>
<td align="center">10</td>
</tr>
<tr>
<td align="center">3x8</td>
<td align="center">11</td>
</tr>
<tr>
<td align="center">2x12</td>
<td align="center">5</td>
</tr>
<tr>
<td align="center">24</td>
<td align="center">6</td>
</tr>
</tbody></table>
The maximum Digital Root Sum  of 24 is 11.<br>The function mdrs(n) gives the maximum Digital Root Sum of n. So  mdrs(24)=11.<br>Find ∑mdrs(n) for 1 &lt; n &lt; 1,000,000.


## 解决方案


## 代码


