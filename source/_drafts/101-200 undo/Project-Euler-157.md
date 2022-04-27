---
title: Project Euler 157
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 157
## 题目
### Solving the diophantine equation <sup>1</sup>/<sub><var>a</var></sub>+<sup>1</sup>/<sub><var>b</var></sub>= <sup><var>p</var></sup>/<sub>10<sup><var>n</var></sup></sub> 

Consider the diophantine equation ^1/_<var>a</var>+^1/_<var>b</var>= ^<var>p</var>/_10^<var>n</var> with <var>a, b, p, n</var> positive integers and <var>a</var> ≤ <var>b</var>.<br />
For <var>n</var>=1 this equation has 20 solutions that are listed below:
<table><tr><td width="120">^1/_1+^1/_1=^20/_10</td>
<td width="120">^1/_1+^1/_2=^15/_10</td>
<td width="120">^1/_1+^1/_5=^12/_10</td>
<td width="120">^1/_1+^1/_10=^11/_10</td>
<td width="120">^1/_2+^1/_2=^10/_10</td>
</tr><tr><td width="120">^1/_2+^1/_5=^7/_10</td>
<td width="120">^1/_2+^1/_10=^6/_10</td>
<td width="120">^1/_3+^1/_6=^5/_10</td>
<td width="120">^1/_3+^1/_15=^4/_10</td>
<td width="120">^1/_4+^1/_4=^5/_10</td>
</tr><tr><td width="120">^1/_4+^1/_20=^3/_10</td>
<td width="120">^1/_5+^1/_5=^4/_10</td>
<td width="120">^1/_5+^1/_10=^3/_10</td>
<td width="120">^1/_6+^1/_30=^2/_10</td>
<td width="120">^1/_10+^1/_10=^2/_10</td>
</tr><tr><td width="120">^1/_11+^1/_110=^1/_10</td>
<td width="120">^1/_12+^1/_60=^1/_10</td>
<td width="120">^1/_14+^1/_35=^1/_10</td>
<td width="120">^1/_15+^1/_30=^1/_10</td>
<td width="120">^1/_20+^1/_20=^1/_10</td>
</tr></table>How many solutions has this equation for 1 ≤ <var>n</var> ≤ 9?


# Project Euler 157
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
  
<b>Solving the diophantine equation ^1/_a+^1/_b= ^p/_10^n </b>
Consider the diophantine equation ^1/_a+^1/_b= ^p/_10^n with a, b, p, n positive integers and a ≤ b.<br>For n=1 this equation has 20 solutions that are listed below:
<table>
<thead>
<tr>
<th align="center">&nbsp;</th>
<th align="center">&nbsp;</th>
<th align="center">&nbsp;</th>
<th align="center">&nbsp;</th>
<th align="center">&nbsp;</th>
</tr>
</thead>
<tbody><tr>
<td align="center">^1/_1+^1/_1=^20/_10</td>
<td align="center">^1/_1+^1/_2=^15/_10</td>
<td align="center">^1/_1+^1/_5=^12/_10</td>
<td align="center">^1/_1+^1/_10=^11/_10</td>
<td align="center">^1/_2+^1/_2=^10/_10</td>
</tr>
<tr>
<td align="center">^1/_2+^1/_5=^7/_10</td>
<td align="center">^1/_2+^1/_10=^6/_10</td>
<td align="center">^1/_3+^1/_6=^5/_10</td>
<td align="center">^1/_3+^1/_15=^4/_10</td>
<td align="center">^1/_4+^1/_4=^5/_10</td>
</tr>
<tr>
<td align="center">^1/_4+^1/_20=^3/_10</td>
<td align="center">^1/_5+^1/_5=^4/_10</td>
<td align="center">^1/_5+^1/_10=^3/_10</td>
<td align="center">^1/_6+^1/_30=^2/_10</td>
<td align="center">^1/_10+^1/_10=^2/_10</td>
</tr>
<tr>
<td align="center">^1/_11+^1/_110=^1/_10</td>
<td align="center">^1/_12+^1/_60=^1/_10</td>
<td align="center">^1/_14+^1/_35=^1/_10</td>
<td align="center">^1/_15+^1/_30=^1/_10</td>
<td align="center">^1/_20+^1/_20=^1/_10</td>
</tr>
</tbody></table>
How many solutions has this equation for 1 ≤ n ≤ 9?


## 解决方案


## 代码


