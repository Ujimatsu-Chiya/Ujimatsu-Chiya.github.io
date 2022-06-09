---
title: Project Euler 652
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 652
## 题目
### Distinct values of a proto-logarithmic function

Consider the values of $\log_2(8)$, $\text{log}_4(64)$ and $\text{log}_3(27)$. All three are equal to $3$.

Generally, the function $f(m,n)=\text{log}_m(n)$ over integers $m,n \ge 2$ has the property that <br />
$f(m_1,n_1)=f(m_2,n_2)$ if
<ol><li>$\, m_1=a^e, n_1=a^f, m_2=b^e,n_2=b^f \,$ for some integers $a,b,e,f \, \,$ or </li>
<li> $ \, m_1=a^e, n_1=b^e, m_2=a^f,n_2=b^f \,$ for some integers $a,b,e,f \,$ </li></ol>We call a function $g(m,n)$ over integers $m,n \ge 2$ <i>proto-logarithmic</i>  if 
<ul><li>$\quad  \, \, \, \, g(m_1,n_1)=g(m_2,n_2)$ if any integers $a,b,e,f$ fulfilling 1. or 2. can be found </li>
<li><b>and</b> $\, g(m_1,n_1) \ne g(m_2,n_2)$ if no integers $a,b,e,f$ fulfilling 1. or 2. can be found</li>
</ul>Let $D(N)$ be the number of distinct values that any proto-logarithmic function $g(m,n)$ attains over $2\le m, n\le N$.<br />
For example, $D(5)=13$, $D(10)=69$, $D(100)=9607$ and $D(10000)=99959605$.

Find $D(10^{18})$, and give the last 9 digits as answer.


<br /><font size="2"><b>Note:</b> According to the <b>four exponentials conjecture</b> the function $\text{log}_m(n)$ is <i>proto-logarithmic</i>.<br /> While this conjecture is yet unproven in general, $\text{log}_m(n)$ can be used to calculate $D(N)$ for small values of $N$.</font>


# Project Euler 652
## 题目
### Distinct values of a proto-logarithmic function

Consider the values of $\log_2(8)$, $\log_4(64)$ and $\log_3(27)$. All three are equal to $3$.
Generally, the function $f(m,n)=\log_m(n)$ over integers $m,n\ge 2$ has the property that<br>$f(m_1,n_1)=f(m_2,n_2)$ if
<ol>
<li>$m_1=a^e$, $n_1=a^f$, $m_2=b^e$, $n_2=b^f$ for some integers $a, b, e, f$ or</li>
<li>$m_1=a^e$, $n_1=b^e$, $m_2=a^f$, $n_2=b^f$ for some integers $a, b, e, f$</li>
</ol>
We call a function $g(m,n)$ over integers $m,n\ge 2$ <i>proto-logarithmic</i> if
<ul>
<li>$g(m_1,n_1) = g(m_2,n_2)$ if any integers $a, b, e, f$ fulfilling 1. or 2. can be found</li>
<li>**and** $g(m_1,n_1)\neq g(m_2,n_2)$ if no integers $a, b, e, f$ fulfilling 1. or 2. can be found</li>
</ul>
Let $D(N)$ be the number of distinct values that any proto-logarithmic function $g(m,n)$ attains over $2\le m,n\le N$.<br>For example, $D(5)=13$, $D(10)=69$, $D(100)=9607$ and $D(10000)=99959605$.
Find $D(10^{18})$, and give the last $9$ digits as answer.
**Note**: According to the **four exponentials conjecture** the function $\log_m(n)$ is <i>proto-logarithmic</i>. While this conjecture is yet unproven in general, $\log_m(n)$ can be used to calculate $D(N)$ for small values of $N$.


## 解决方案


## 代码


