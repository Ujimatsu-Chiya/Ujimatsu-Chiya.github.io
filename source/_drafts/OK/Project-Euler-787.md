---
title: Project Euler 787
category:
  - Project Euler
tags:
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 787
## 题目
### Bézout's Game


Two players play a game with two piles of stones. They take alternating turns. If there are currently $a$ stones in the first pile and $b$ stones in the second, a turn consists of removing $c\geq 0$ stones from the first pile and $d\geq 0$ from the second in such a way that $ad-bc=\pm1$. The winner is the player who first empties one of the piles.

Note that the game is only playable if the sizes of the two piles are coprime.

A game state $(a, b)$ is a winning position if the next player can guarantee a win with optimal play. Define $H(N)$ to be the number of winning positions $(a, b)$ with $\gcd(a,b)=1$, $a > 0$, $b > 0$ and $a+b \leq N$. Note the order matters, so for example $(2,1)$ and $(1,2)$ are distinct positions.

You are given $H(4)=5$ and $H(100)=2043$.

Find $H(10^9)$.


## 解决方案

通过以下程序打表：

```C++
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N=50;
bool ok[N+4][N+4];
int main(){
    int ans=0;
    for(int a=1;a<=N;a++)
        for(int b=a;b<=N;b++){
            if(__gcd(a,b)!=1) continue;
            if(a>b) ok[a][b]=ok[b][a];
            else{
                for(int c=0;c<=a&&!ok[a][b];c++){
                    if((b*c+1)%a==0){
                        int d=(b*c+1)/a;
                        if(d<=b&&!ok[a-c][b-d]) ok[a][b]=1;
                    }
                    if((b*c-1)%a==0){
                        int d=(b*c-1)/a;
                        if(d<=b&&!ok[a-c][b-d]) ok[a][b]=1;
                    }
                }
            }
            if(ok[a][b]) ++ans,printf("%d %d\n",a,b);
        }
    printf("%d\n",ans);
}

```

发现如果当前局面是必胜态，当且仅当$\min(a,b)$是奇数。

## 代码


