---
title: Project Euler 630
tags:
  - Project Euler
mathjax: true
date: 2022-07-13 22:57:40
---

<escape><!-- more --></escape>

# Project Euler 630

## 题目

### Crossed lines

Given a set, $L$, of unique lines, let $M(L)$ be the number of lines in the set and let $S(L)$ be the sum over every line of the number of times that line is crossed by another line in the set.  For example, two sets of three lines are shown below:

![](../images/p630_threelines.png)

In both cases M(L) is 3 and S(L) is 6: each of the three lines is crossed by two other lines.  Note that even if the lines cross at a single point, all of the separate crossings of lines are counted.

Consider points $(T_{2k−1}, T_{2k})$, for integer $k \ge 1$, generated in the following way:

$\begin{aligned}
S_0  &=   290797\\
S_{n+1}  &=   {S_n}^2 \mod 50515093\\
T_n  &=   ( S_n \mod 2000 ) − 1000
\end{aligned}$

For example, the first three points are: $(527, 144), (−488, 732), (−454, −947)$.  Given the first $n$ points generated in this manner, let $L_n$ be the set of **unique** lines that can be formed by joining each point with every other point, the lines being extended indefinitely in both directions.  We can then define $M(L_n)$ and $S(L_n)$ as described above.

For example, $M(L_3) = 3$ and $S(L_3) = 6$.  Also $M(L_{100}) = 4948$ and $S(L_{100}) = 24477690$.

Find $S(L_{2500})$.

## 解决方案

斜率相同的两条的直线永远不会相交，斜率不相同那么两条直线就会相交。

将每条斜率相同的直线划分汇集到一起，假设为$k_i$条。如果一共有$n$组斜率两两不相同的直线，那么$M(L)=\sum_{i=1}^nk_i$，并且$S(L)=\sum_{i=1}^n k_i\cdot (M(L)-k_i)$。

实现时，每一条直线都分别用两个点表示，因此引出两个问题：不同斜率的直线如何分类，以及如何对直线进行去重。

为解决第一个问题，我们为这一些直线进行“定向”,即为沿着直线的两个方向指定一个向量。斜率相同的直线，定的方向都相同。然后就将这些直线将它们定下的方向向量作为关键字进行极角排序，排序完成后，相邻两条直线对应向量叉积若为$0$，那么说明它们是同一斜率下的。

为解决第二个问题，考虑两条斜率相同的直线$P_1P_2$和$Q_1Q_2$是否为同一直线，并且已经定向成$\overrightarrow{P_1P_2},\overrightarrow{Q_1Q_2}$。为了方便第二步去重，首先极角排序时就需要内部处理好斜率相同时直线的位置。如果$\overrightarrow{P_1P_2}\times\overrightarrow{P_1Q_1}>0$，那么说明直线$Q_1Q_2$在$P_1P_2$的左（上）边。因此极角排序时，还需要以$\overrightarrow{P_1P_2}\times\overrightarrow{P_1Q_1}$的正负性作为第二关键字进行排序。最终去重时，如果$\overrightarrow{P_1P_2}\times\overrightarrow{P_1Q_1}=0$，那么说明两条直线其实是同一条，并去除。

## 代码

```C++
# include <bits/stdc++.h>
# define pi pair<int,int>
using namespace std;
typedef long long ll;
const int N=2500;
int S[N*2+4],T[N*2+4];
struct P {
    ll x, y;
    // 向量减法
    P(ll xx=0,ll yy=0):x(xx),y(yy){}
    P operator-(P p) const {
        return {x - p.x, y - p.y};
    }
    // 向量叉积
    ll operator^(P p) const {
        return x * p.y - y * p.x;
    }
    bool operator < (P&p) const{
        return x<p.x||x==p.x&&y<p.y;
    }
}p[N+4];
struct L {
    P p1, p2;
    L(){}
    L(P p1, P p2) {
        this->p1 = p1;
        this->p2 = p2;
    }
    P vec(){return p2-p1;}
    bool operator ==(L &l){
        return ((vec())^(l.vec()))==0&&(vec()^(l.p1-p1))==0;
    }
    bool operator < (L &l){
        ll v=((vec())^(l.vec()));
        if(v!=0) return v<0;
        return (vec()^(l.p1-p1))<0;
    }

}l[N*(N-1)/2+4];
int np=0,nl=0;
int main(){
    S[0]=290797;
    for(int i=1;i<=N*2;i++){
        S[i]=1ll*S[i-1]*S[i-1]%50515093;
        T[i]=S[i]%2000-1000;
    }
    for(int i=2;i<=N+N;i+=2)
        p[++np]=P(T[i-1],T[i]);
    sort(p+1,p+np+1);
    for(int i=1;i<=N;i++)
        for(int j=i+1;j<=N;j++)
            l[++nl]=L(p[i],p[j]);
    sort(l+1,l+nl+1);
    nl=unique(l+1,l+nl+1)-l-1;
    ll ans=1ll*nl*(nl-1);
    for(int i=1,j=1;i<=nl;i=j){
        for(;j<=nl&&(l[i].vec()^l[j].vec())==0;++j);
        ans-=1ll*(j-i)*(j-i-1);
    }
    printf("%lld\n",ans);
}

```
