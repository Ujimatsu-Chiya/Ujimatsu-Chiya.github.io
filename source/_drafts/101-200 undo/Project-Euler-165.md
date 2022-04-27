---
title: Project Euler 165
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 165
## 题目
### Intersections

A segment is uniquely defined by its two endpoints.<br /> By considering two line segments in plane geometry there are three possibilities:<br /> 
the segments have zero points, one point, or infinitely many points in common.
Moreover when two segments have exactly one point in common it might be the case that that common point is an endpoint of either one of the segments or of both. If a common point of two segments is not an endpoint of either of the segments it is an interior point of both segments.<br />
We will call a common point T of two segments L_1 and L_2 a true intersection point of L_1 and L_2  if T is the only common point of L_1 and L_2  and T is an interior point of both segments.

Consider the three segments L_1, L_2, and L_3:
<p class="margin_left">L_1: (27, 44) to (12, 32)<br />
L_2: (46, 53) to (17, 62)<br />
L_3: (46, 70) to (22, 40)
It can be verified that line segments L_2 and L_3 have a true intersection point. We note that as the one of the end points of L_3: (22,40) lies on L_1 this is not considered to be a true point of intersection. L_1 and L_2 have no common point. So among the three line segments, we find one true intersection point.
Now let us do the same for 5000 line segments. To this end, we generate 20000 numbers using the so-called "Blum Blum Shub" pseudo-random number generator.
<p class="margin_left">s_0 = 290797<br /><br />
s_n+1 = s_n×s_n (modulo 50515093)<br /><br />
t_n = s_n (modulo 500)
To create each line segment, we use four consecutive numbers t_n. That is, the first line segment is given by:
(t_1, t_2) to (t_3, t_4)
The first four numbers computed according to the above generator should be: 27, 144, 12 and 232. The first segment would thus be (27,144) to (12,232).
How many distinct true intersection points are found among the 5000 line segments?



# Project Euler 165
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
  
<b>Intersections</b>
A segment is uniquely defined by its two endpoints. By considering two line segments in plane geometry there are three possibilities:<br>the segments have zero points, one point, or infinitely many points in common.
Moreover when two segments have exactly one point in common it might be the case that that common point is an endpoint of either one of the segments or of both. If a common point of two segments is not an endpoint of either of the segments it is an interior point of both segments.<br>We will call a common point T of two segments L_1 and L_2 a true intersection point of L_1 and L_2  if T is the only common point of L_1 and L_2  and T is an interior point of both segments.
Consider the three segments L_1, L_2, and L_3:
L_1: (27, 44) to (12, 32)<br>L_2: (46, 53) to (17, 62)<br>L_3: (46, 70) to (22, 40)
It can be verified that line segments L_2 and L_3 have a true intersection point. We note that as the one of the end points of L_3: (22,40) lies on L_1 this is not considered to be a true point of intersection. L_1 and L_2 have no common point. So among the three line segments, we find one true intersection point.
Now let us do the same for 5000 line segments. To this end, we generate 20000 numbers using the so-called “Blum Blum Shub” pseudo-random number generator.
s_0 = 290797<br>s_n+1 = s_n×s_n (modulo 50515093)<br>t_n = s_n (modulo 500)
To create each line segment, we use four consecutive numbers t_n. That is, the first line segment is given by:
(t_1, t_2) to (t_3, t_4)
The first four numbers computed according to the above generator should be: 27, 144, 12 and 232. The first segment would thus be (27,144) to (12,232).
How many distinct true intersection points are found among the 5000 line segments?


## 解决方案


## 代码


