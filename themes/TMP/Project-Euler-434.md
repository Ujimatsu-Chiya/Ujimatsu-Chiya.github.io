---
title: Project Euler 434
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 434
## 题目
### Rigid graphs

Recall that a graph is a collection of vertices and edges connecting the vertices, and that two vertices connected by an edge are called adjacent.<br />
Graphs can be embedded in Euclidean space by associating each vertex with a point in the Euclidean space.<br />
A **flexible** graph is an embedding of a graph where it is possible to move one or more vertices continuously so that the distance between at least two nonadjacent vertices is altered while the distances between each pair of adjacent vertices is kept constant.<br />
A **rigid** graph is an embedding of a graph which is not flexible.<br />
Informally, a graph is rigid if by replacing the vertices with fully rotating hinges and the edges with rods that are unbending and inelastic, no parts of the graph can be moved independently from the rest of the graph.

The **grid graphs** embedded in the Euclidean plane are not rigid, as the following animation demonstrates:
<div class="center"><img src="project/images/p434_rigid.gif" class="dark_img" alt="p434_rigid.gif" /></div>
However, one can make them rigid by adding diagonal edges to the cells. For example, for the 2x3 grid graph, there are 19 ways to make the graph rigid:
<div class="center"><img src="project/images/p434_rigid23.png" class="dark_img" alt="p434_rigid23.png" /></div>
Note that for the purposes of this problem, we do not consider changing the orientation of a diagonal edge or adding both diagonal edges to a cell as a different way of making a grid graph rigid.

Let <var>R</var>(<var>m</var>,<var>n</var>) be the number of ways to make the <var>m</var> \times <var>n</var> grid graph rigid. <br />
E.g. <var>R</var>(2,3) = 19 and <var>R</var>(5,5) = 23679901

Define <var>S</var>(<var>N</var>) as <span style="font-size:larger;"><span style="font-size:larger;">\sum</span></span> <var>R</var>(<var>i</var>,<var>j</var>) for 1 \le <var>i</var>, <var>j</var> \le <var>N</var>.<br />
E.g. <var>S</var>(5) = 25021721.<br />
Find <var>S</var>(100), give your answer modulo 1000000033.



# Project Euler 434
## 题目
### Rigid graphs

Recall that a graph is a collection of vertices and edges connecting the vertices, and that two vertices connected by an edge are called adjacent.<br>Graphs can be embedded in Euclidean space by associating each vertex with a point in the Euclidean space.<br>A **flexible** graph is an embedding of a graph where it is possible to move one or more vertices continuously so that the distance between at least two nonadjacent vertices is altered while the distances between each pair of adjacent vertices is kept constant.<br>A **rigid** graph is an embedding of a graph which is not flexible.<br>Informally, a graph is rigid if by replacing the vertices with fully rotating hinges and the edges with rods that are unbending and inelastic, no parts of the graph can be moved independently from the rest of the graph.
The **grid graphs** embedded in the Euclidean plane are not rigid, as the following animation demonstrates:
<center><img src="https://projecteuler.net/project/images/p434_rigid.gif"></center>

However, one can make them rigid by adding diagonal edges to the cells. For example, for the 2x3 grid graph, there are 19 ways to make the graph rigid:
<center><img src="https://projecteuler.net/project/images/p434_rigid23.png"></center>

Note that for the purposes of this problem, we do not consider changing the orientation of a diagonal edge or adding both diagonal edges to a cell as a different way of making a grid graph rigid.
Let R(m,n) be the number of ways to make the m \times n grid graph rigid.<br>E.g. R(2,3) = 19 and R(5,5) = 23679901
Define S(N) as \sumR(i,j) for 1 \le i, j \le N.<br>E.g. S(5) = 25021721.<br>Find S(100), give your answer modulo 1000000033


## 解决方案


## 代码


