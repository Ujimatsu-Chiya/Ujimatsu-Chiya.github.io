---
title: Project Euler 155
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 155
## 题目
### Counting Capacitor Circuits

An electric circuit uses exclusively identical capacitors of the same value C.
<br />
The capacitors can be connected in series or in parallel to form sub-units, which can then be connected in series or in parallel with other capacitors or other sub-units to form larger sub-units, and so on up to a final circuit.
Using this simple procedure and up to <var>n</var> identical capacitors, we can make circuits having a range of different total capacitances. For example, using up to <var>n</var>=3 capacitors of 60 $\mu$ F each, we can obtain the following 7 distinct total capacitance values: 
<div class="center"><img src="project/images/p155_capacitors1.gif" class="dark_img" alt="" />

# Project Euler 155
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
  
<b>Counting Capacitor Circuits</b>
An electric circuit uses exclusively identical capacitors of the same value C.<br>The capacitors can be connected in series or in parallel to form sub-units, which can then be connected in series or in parallel with other capacitors or other sub-units to form larger sub-units, and so on up to a final circuit.
Using this simple procedure and up to n identical capacitors, we can make circuits having a range of different total capacitances. For example, using up to n=3 capacitors of 60μF each, we can obtain the following 7 distinct total capacitance values: 
<center><img src="https://projecteuler.net/project/images/p155_capacitors1.gif" width="387" height="557" alt=""></center>

If we denote by D(n) the number of distinct total capacitance values we can obtain when using up to n equal-valued capacitors and the simple procedure described above, we have: D(1)=1, D(2)=3, D(3)=7 \dots
Find D(18).
<em>Reminder :</em> When connecting capacitors C_1, C_2 etc in parallel, the total capacitance is C_T&nbsp;=&nbsp;C_1&nbsp;+&nbsp;C_2&nbsp;+\dots,<br>whereas when connecting them in series, the overall capacitance is given by:$\frac{1}{C_T}=\frac{1}{C_1}+\frac{1}{C_2}+\dots$.


## 解决方案


## 代码


