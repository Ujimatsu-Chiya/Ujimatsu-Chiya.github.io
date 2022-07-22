---
title: Project Euler 649
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 649
## 题目
### Low-Prime Chessboard Nim


Alice and Bob are taking turns playing a game consisting of $c$ different coins on a chessboard of size $n$ by $n$.

The game may start with any arrangement of $c$ coins in squares on the board. It is possible at any time for more than one coin to occupy the same square on the board at the same time. The coins are distinguishable, so swapping two coins gives a different arrangement if (and only if) they are on different squares.

On a given turn, the player must choose a coin and move it either left or up $2$, $3$, $5$, or $7$ spaces in a single direction. The only restriction is that the coin cannot move off the edge of the board.

The game ends when a player is unable to make a valid move, thereby granting the other player the victory.

Assuming that Alice goes first and that both players are playing optimally, let $M(n, c)$ be the number of possible starting arrangements for which Alice can ensure her victory, given a board of size $n$ by $n$ with $c$ distinct coins.

For example, $M(3, 1) = 4$, $M(3, 2) = 40$, and $M(9, 3) = 450304$.

What are the last $9$ digits of $M(10\,000\,019, 100)$?





## 解决方案
```C++
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N=40,M=500;
int sg[N+4],c[8];
bool mex[144];
vector<int>z{2,3,5,7};
int main(){
    for(int i=1;i<=N;i++){
        memset(mex,0,sizeof(mex));
        for(int x:z)
            if(i-x>0) mex[sg[i-x]]=1;
        int j=0;
        for(;mex[j];++j);
        sg[i]=j;
    }
}

```

## 代码


```C++
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N=10000019;
const int C=100;
const int D=1<<3;
ll mod=1000000000;
int sg[10]={0,0,0,1,1,2,2,3,3,4};
ll cnt[D];
ll a[D],b[D];
void cal(ll a[D],ll b[D],ll ans[D]){
    ll c[D]={0};
    for(int i=0;i<D;i++)
        for(int j=0;j<D;j++)
            c[i^j]=(c[i^j]+a[i]*b[j])%mod;
    memcpy(ans,c,sizeof(c));
}
int main(){
    for(int i=1;i<=9;i++)
        cnt[sg[i]]+=(N+9-i)/9%mod;
    cal(cnt,cnt,b);
    a[0]=1;
    for(int c=C;c;c>>=1){
        if(c&1) cal(a,b,a);
        cal(b,b,b);
    }
    ll ans=0;
    for(int i=1;i<D;i++)
        ans=(ans+a[i])%mod;
    printf("%lld\n",ans);
}

```