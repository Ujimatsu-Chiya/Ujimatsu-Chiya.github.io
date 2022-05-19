---
title: Project Euler 196
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
  

# Project Euler 196
## 题目
### Prime triplets

Build a triangle from all positive integers in the following way:
||||||||||||
|-|-|-|-|-|-|-|-|-|-|-|
|$1$|||||||||||
|$\color{red}{2}$|$\color{red}{3}$||||||||||
|$4$|$\color{red}{5}$|$6$|||||||||
|$\color{red}{7}$|$8$|$9$|$10$||||||||
|$\color{red}{11}$|$12$|$\color{red}{13}$|$14$|$15$|||||||
|$16$|$\color{red}{17}$|$18$|$\color{red}{19}$|$20$|$21$||||||
|$22$|$\color{red}{23}$|$24$|$25$|$26$|$27$|$28$|||||
|$\color{red}{29}$|$30$|$\color{red}{31}$|$32$|$33$|$34$|$35$|$36$||||
|$\color{red}{37}$|$38$|$39$|$40$|$\color{red}{41}$|$42$|$\color{red}{43}$|$44$|$45$|||
|$46$|$\color{red}{47}$|$48$|$49$|$50$|$51$|$52$|$\color{red}{53}$|$54$|$55$||
|$56$|$57$|$58$|$\color{red}{59}$|$60$|$\color{red}{61}$|$62$|$63$|$64$|$65$|$66$|
|$\dots$|$\dots$|$\dots$|||||||||

Each positive integer has up to eight neighbours in the triangle.

A set of three primes is called a *prime triplet* if one of the three primes has the other two as neighbours in the triangle.

For example, in the second row, the prime numbers $2$ and $3$ are elements of some prime triplet.

If row $8$ is considered, it contains two primes which are elements of some prime triplet, i.e. $29$ and $31$.

If row $9$ is considered, it contains only one prime which is an element of some prime triplet: $37$.

Define $S(n)$ as the sum of the primes in row $n$ which are elements of any prime triplet. Then $S(8)=60$ and $S(9)=37$.

You are given that $S(10000)=950007619$.

Find $S(5678027) + S(7208785)$.


## 解决方案

如果要求第$S(N)$，为确保第$N$行的在质数三元组的数都能够被找到，第$N-2$行到第$N+2$的所有质数都需要每局出来。假设第$N-2$行的第一个质数为$L$，第$N+2$行的最后一个质数为$R$。

第一个问题：找到$L,R$之间的所有质数。

不难发现，虽然$L,R$是$O(n^2)$级别的，但是$R-L$却是$O(n)$级别的。另外，$L,R$之间的合数一定被$\lfloor\sqrt{R}\rfloor$以内的质因数解决。这启发了我们用两次质数筛法解决：

1. 先用一般的埃氏筛法找到$\lfloor\sqrt{R}\rfloor$以内的质数。
2. 将第一步筛出来的质数用于筛掉$L,R$之间的合数。这里的实现需要注意一些细节，如数组的偏移量是$L$；如果是用质数$p$来筛合数，那么要从$\lceil\dfrac{L}{p}\rceil\cdot p$开始筛起。

第二个问题：求解原问题答案。

对于第$N$行的每一个数**质数**$n$而言，以它为中心的$5\times5$方格内的数都是它的判断对象，如下图（色为内圈，色为外圈）：

$n$为答案的条件满足这两个之一：内圈中有两个是质数；内圈和外圈中一对有公共边或角（如上图深色部分）的数都是质数。

因此为了解决第二个问题，可以先将这一对有公共边和角的数的**相对坐标**全都预处理出来，直接判断。

本问题还有一些细节，实现时需要注意。

## 代码


```C++
#include <bits/stdc++.h>
# define pi pair<int,int>
using namespace std;
typedef long long ll;
const int Q1=5678027,Q2=7208785;
bool b[Q2*5+2];
ll pr[Q2 + 104];
int p=0;
//对应8个方向中再向外走一步的格子的方向。不难发现，如果当前是质数，那么左边和右边一定是偶数，这可以排除左右两个方向。
vector<pi>dr[3][3];
int dx[8]={-1,-1,-1,0,0,1,1,1},dy[8]={-1,0,1,-1,1,-1,0,1};
ll st(ll n){
    return n*(n-1)/2+1;
}
//判断第n+d行第y列的数是否为质数。
bool is_prime(int n, int d, int y){
    if(y<0||y>=n+d) return false;
    else{
        n-=2;d+=2;
        return !b[y+(n+n+d-1)*d/2];
    }
}
//判断第n第y个质数是不是所求答案。
bool is_answer(int n,int y){
    if(!is_prime(n, 0, y)) return false;
    int cnt=0;
    for(int k=0;k<8;k++){
        if(dx[k]==0) continue;
        if(is_prime(n, dx[k], y + dy[k])){
            if(++cnt>=2) return true;
            for(auto &[ox,oy]:dr[dx[k]+1][dy[k]+1]){
                if(is_prime(n, ox, y + oy)) return true;
            }
        }
    }
    return false;
}
ll solve(int row){
    ll l=st(row-2),r=st(row+3)-1;
    ll sq=sqrt(r);
    p=0;
    memset(b,0,sizeof(b));
    for(int i=2;i<=sq;i++){
        if(b[i]) continue;
        pr[++p]=i;
        for(int j=i;1ll*i*j<=sq;j++)
            b[i*j]=true;
    }
    memset(b,0,sizeof(b));
    for(int i=1; i <= p; i++)
        for(ll j= (l + pr[i] - 1) / pr[i]; j * pr[i] <= r; j++)
            b[j * pr[i] - l]=true;
    ll ans=0,nl=st(row);
    for(int y=0;y<row;y++)
        if(is_answer(row,y)) ans+=nl+y;
    return ans;
}
int main(){
    for(int i=-1;i<=1;i++){
        for(int j=-1;j<=1;j++){
            if(i==0) continue;
            for(int k=0;k<8;k++){
                int x=i+dx[k],y=j+dy[k];
                if(max(abs(x),abs(y))==2){
                    dr[i+1][j+1].push_back(pi(x,y));
                }
            }
        }
    }
    ll ans = solve(Q1) + solve(Q2);
    printf("%lld\n",ans);
}

```