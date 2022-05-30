---
title: Project Euler 213
tags:
  - Project Euler
  - 概率
  - 动态规划
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 213
## 题目
### Flea Circus


A $30\times30$ grid of squares contains $900$ fleas, initially one flea per square.

When a bell is rung, each flea jumps to an adjacent square at random (usually $4$ possibilities, except for fleas on the edge of the grid or at the corners).

What is the expected number of unoccupied squares after $50$ rings of the bell? Give your answer rounded to six decimal places.


## 解决方案

令$N=30,M=50$。单独考虑$N\times N$方格中每个格子上的跳蚤最终跳去的地方，使用动态规划的思想解决。

令$f_{n,m}(i,j,k)(0\le i\le M,0\le j,n< N,0\le k,m < N)$表示从格子$(n,m)$经过$i$步走到格子$(j,k)$的概率。那么，可以列出以下状态转移方程：

$$
f_{n,m}(i,j,k)=
\left \{\begin{aligned}
  &1 & & \mathrm{if\quad} i=0\&j=n\&k=m \\
  &0 & & \mathrm{else if\quad} i=0 \\
  &\sum_{x,y,|j-x|+|k-y|=1,0\le x,y<N}\dfrac{f_{n,m}(i-1,x,y)}{\text{dir}(x,y)} & & \mathrm{else}
\end{aligned}\right.
$$

其中，函数$\text{dir}(x,y)$表示从格子$(x,y)$可以跳往的方向数。

方程的最后一行说明，在状态$f_{n,m}(i-1,x,y)$时，有$\text{dir}(x,y)$的概率跳向$(j,k)$。

那么，独立地看单独一个格子$(n,m)$。根据乘法原理，它上面没有跳蚤的概率为：

$$p(n,m)=\prod_{i=0}^{N-1}\prod_{j=0}^{M-1}f_{i,j}(M,n,m)$$

因此，最终答案即为期望之和，也就是

$$\sum_{i=0}^{N-1}\sum_{j=0}^{M-1}p(i,j)$$

注意到，由于正方形是对称的，因此本代码只计算了约$\dfrac{1}{4}$的格子后就可以求出$p$。如果加上对角线的对称轴，只需要计算$\dfrac{1}{8}$的格子即可。

## 代码


```C++
#include <bits/stdc++.h>
using namespace std;
const int N=30,M=50;
int dx[4]={-1,1,0,0},dy[4]={0,0,-1,1};
double f[M+1][N][N],g[N][N];
int dir[N][N];
void solve(int x,int y){
    memset(f,0,sizeof(f));
    f[0][x][y]=1;
    for(int i=1;i<=M;i++)
        for(int j=0;j<N;j++)
            for(int k=0;k<N;k++){
                for(int r=0;r<4;r++){
                    int x=j+dx[r],y=k+dy[r];
                    if(x>=0&&y>=0&&x<N&&y<N) f[i][j][k]+=f[i-1][x][y]/dir[x][y];
                }
            }
    for(int i=0;i<N;i++)
        for(int j=0;j<N;j++) {
            g[i][j] *= 1.0 - f[M][i][j];
            if(i!=N-1-i) g[i][j] *= 1.0 - f[M][N-1-i][j];
            if(j!=N-1-j) g[i][j] *= 1.0 - f[M][i][N-1-j];
            if(i!=N-1-i&&j!=N-1-j) g[i][j] *= 1.0 - f[M][N-1-i][N-1-j];
        }
}
int main(){
    clock_t a = clock();
    for(int i=0;i<N;i++)
        for(int j=0;j<N;j++) {
            g[i][j] = 1;
            for (int k = 0; k < 4; k++) {
                int x = i + dx[k], y = j + dy[k];
                if (x >= 0 && y >= 0 && x < N && y < N) ++dir[i][j];
            }
        }
    for(int i=0;i<(N+1)/2;i++)
        for(int j=0;j<(N+1)/2;j++)
            solve(i,j);
    double ans=0;
    for(int i=0;i<N;i++)
        for(int j=0;j<N;j++)
            ans+=g[i][j];
    printf("%.6f\n",ans);
    cout << clock() - a << endl;
}

```