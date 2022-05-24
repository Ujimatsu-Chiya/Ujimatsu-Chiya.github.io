---
title: Project Euler 623
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 623
## 题目
### Lambda Count

The <i>lambda-calculus</i> is a universal model of computation at the core of functional programming languages. It is based on <i>lambda-terms</i>, a minimal programming language featuring only function definitions, function calls and variables. Lambda-terms are built according to the following rules:
<ul><li>Any <i>variable</i> $x$ (single letter, from some infinite alphabet) is a lambda-term.</li>
<li>If $M$ and $N$ are lambda-terms, then $(M N)$ is a lambda-term, called the <i>application</i> of $M$ to $N$.</li>
<li>If $x$ is a variable and $M$ is a term, then $(\lambda x. M)$ is a lambda-term, called an <i>abstraction</i>. An abstraction defines an anonymous function, taking $x$ as parameter and sending back $M$.</li>
</ul>A lambda-term $T$ is said to be <i>closed</i> if for all variables $x$, all occurrences of $x$ within $T$ are contained within some abstraction $(\lambda x. M)$ in $T$. The smallest such abstraction is said to <i>bind</i> the occurrence of the variable $x$. In other words, a lambda-term is closed if all its variables are bound to parameters of enclosing functions definitions. For example, the term $(\lambda x. x)$ is closed, while the term $(\lambda x. (x y))$ is not because $y$ is not bound.

Also, we can rename variables as long as no binding abstraction changes. This means that $(\lambda x. x)$ and $(\lambda y. y)$ should be considered equivalent since we merely renamed a parameter. Two terms equivalent modulo such renaming are called <i>$\alpha$-equivalent</i>. Note that $(\lambda x. (\lambda y. (x y)))$ and $(\lambda x. (\lambda x. (x x)))$ are not $\alpha$-equivalent, since the abstraction binding the first variable was the outer one and becomes the inner one. However, $(\lambda x. (\lambda y. (x y)))$ and $(\lambda y. (\lambda x. (y x)))$ are $\alpha$-equivalent.

The following table regroups the lambda-terms that can be written with at most $15$ symbols, symbols being parenthesis, $\lambda$, dot and variables.

\[\begin{array}{|c|c|c|c|}
\hline
(\lambda x.x) &amp; (\lambda x.(x x)) &amp; (\lambda x.(\lambda y.x)) &amp; (\lambda x.(\lambda y.y)) \\
\hline
(\lambda x.(x (x x))) &amp; (\lambda x.((x x) x)) &amp; (\lambda x.(\lambda y.(x x))) &amp; (\lambda x.(\lambda y.(x y))) \\
\hline
(\lambda x.(\lambda y.(y x))) &amp; (\lambda x.(\lambda y.(y y))) &amp; (\lambda x.(x (\lambda y.x))) &amp; (\lambda x.(x (\lambda y.y))) \\
\hline
(\lambda x.((\lambda y.x) x)) &amp; (\lambda x.((\lambda y.y) x)) &amp; ((\lambda x.x) (\lambda x.x)) &amp; (\lambda x.(x (x (x x)))) \\
\hline
(\lambda x.(x ((x x) x))) &amp; (\lambda x.((x x) (x x))) &amp; (\lambda x.((x (x x)) x)) &amp; (\lambda x.(((x x) x) x)) \\
\hline
\end{array}\]

Let be $\Lambda(n)$ the number of distinct closed lambda-terms that can be written using at most $n$ symbols, where terms that are $\alpha$-equivalent to one another should be counted only once. You are given that $\Lambda(6) = 1$, $\Lambda(9) = 2$, $\Lambda(15) = 20$ and $\Lambda(35) = 3166438$.
Find $\Lambda(2000)$. Give the answer modulo $1\,000\,000\,007$.



# Project Euler 623
## 题目
### Lambda Count

The <i>lambda-calculus</i> is a universal model of computation at the core of functional programming languages. It is based on <i>lambda-terms</i>, a minimal programming language featuring only function definitions, function calls and variables. Lambda-terms are built according to the following rules:
<ul>
<li>Any variable $x$ (single letter, from some infinite alphabet) is a lambda-term.</li>
<li>If $M$ and $N$ are lambda-terms, then $(MN)$ is a lambda-term, called the <i>application</i> of $M$ to $N$.</li>
<li>If $x$ is a variable and $M$ is a term, then $(\lambda x.M)$ is a lambda-term, called an <i>abstraction</i>. An abstraction defines an anonymous function, taking $x$ as parameter and sending back $M$.</li>
</ul>
A lambda-term $T$ is said to be <i>closed</i> if for all variables $x$, all occurrences of $x$ within $T$ are contained within some abstraction $(\lambda x.M)$ in $T$. The smallest such abstraction is said to <i>bind</i> the occurrence of the variable $x$. In other words, a lambda-term is closed if all its variables are bound to parameters of enclosing functions definitions. For example, the term $(\lambda x.x)$ is closed, while the term $(\lambda x.(xy))$ is not because $y$ is not bound.
Also, we can rename variables as long as no binding abstraction changes. This means that $(\lambda x.x)$ and $(\lambda y.y)$ should be considered equivalent since we merely renamed a parameter. Two terms equivalent modulo such renaming are called <i>$\alpha$-equivalent</i>. Note that $(\lambda x.(\lambda y.(xy)))$ and $(\lambda x.(\lambda x.(xx)))$ are not $\alpha$-equivalent, since the abstraction binding the first variable was the outer one and becomes the inner one. However, $(\lambda x.(\lambda y.(xy)))$ and $(\lambda y.(\lambda x.(yx)))$ are $\alpha$-equivalent.
The following table regroups the lambda-terms that can be written with at most $15$ symbols, symbols being parenthesis, $\lambda$, dot and variables.
<table>
<thead>
<tr>
<th></th>
<th></th>
<th></th>
<th></th>
</tr>
</thead>
<tbody><tr>
<td>$(\lambda x.x)$</td>
<td>$(\lambda x.(x(xx)))$</td>
<td>$(\lambda x.(\lambda y.(yx)))$</td>
<td>$(\lambda x.((\lambda y.x)x))$</td>
</tr>
<tr>
<td>$(\lambda x.(x((xx)x)))$</td>
<td>$(\lambda x.(xx))$</td>
<td>$(\lambda x.((xx)x))$</td>
<td>$(\lambda x.(\lambda y.(yy)))$</td>
</tr>
<tr>
<td>$(\lambda x.((\lambda y.y)x))$</td>
<td>$(\lambda x.((xx)(xx)))$</td>
<td>$(\lambda x.(\lambda y.x))$</td>
<td>$(\lambda x.(\lambda y.(xx)))$</td>
</tr>
<tr>
<td>$(\lambda x.(x(\lambda y.x)))$</td>
<td>$((\lambda x.x)(\lambda x.x))$</td>
<td>$(\lambda x.((x(xx))x))$</td>
<td>$(\lambda x.(\lambda y.y))$</td>
</tr>
<tr>
<td>$(\lambda x.(\lambda y.(xy)))$</td>
<td>$(\lambda x.(x(\lambda y.y)))$</td>
<td>$(\lambda x.(x(x(xx))))$</td>
<td>$(\lambda x.(((xx)x)x))$</td>
</tr>
</tbody></table>
Let $\Lambda(n)$ be the number of distinct closed lambda-terms that can be written using at most $n$ symbols, where terms that are $\alpha$-equivalent to one another should be counted only once. You are given that $\Lambda(6)=1$, $\Lambda(9)=2$, $\Lambda(15)=20$ and $\Lambda(35)=3166438$.
Find $\Lambda(2000)$. Give the answer modulo $1000000007$.


## 解决方案


## 代码


