---
title: Project Euler 185
tags:
  - Project Euler
mathjax: true
date: 2022-05-24 11:02:36
---

<escape><!-- more --></escape>

# Project Euler 185

## 题目

### Number Mind

The game Number Mind is a variant of the well known game Master Mind.

Instead of coloured pegs, you have to guess a secret sequence of digits. After each guess you're only told in how many places you've guessed the correct digit. So, if the sequence was $1234$ and you guessed $2036$, you'd be told that you have one correct digit; however, you would NOT be told that you also have another digit in the wrong place.

For instance, given the following guesses for a $5$-digit secret sequence,

90342 ;2 correct<br>
70794 ;0 correct<br>
39458 ;2 correct<br>
34109 ;1 correct<br>
51545 ;2 correct<br>
12531 ;1 correct

The correct sequence $39542$ is unique.

Based on the following guesses,

5616185650518293 ;2 correct<br>
3847439647293047 ;1 correct<br>
5855462940810587 ;3 correct<br>
9742855507068353 ;3 correct<br>
4296849643607543 ;3 correct<br>
3174248439465858 ;1 correct<br>
4513559094146117 ;2 correct<br>
7890971548908067 ;3 correct<br>
8157356344118483 ;1 correct<br>
2615250744386899 ;2 correct<br>
8690095851526254 ;3 correct<br>
6375711915077050 ;1 correct<br>
6913859173121360 ;1 correct<br>
6442889055042768 ;2 correct<br>
2321386104303845 ;0 correct<br>
2326509471271448 ;2 correct<br>
5251583379644322 ;2 correct<br>
1748270476758276 ;3 correct<br>
4895722652190306 ;1 correct<br>
3041631117224635 ;3 correct<br>
1841236454324589 ;3 correct<br>
2659862637316867 ;2 correct

Find the unique 16-digit secret sequence.

## 解决方案

本代码基于深度优先搜索寻找答案，枚举的内容是枚举线索中“**未确定的**正确数位组合”。实现时，使用了嵌套DFS。外层的DFS用于搜索每个线索；内层DFS属于组合枚举，用于寻找“未确定的正确数位组合”。

使用的优化如下：

1. 将每条线索基于正确数量从小到大排序，避免一开始枚举组合的数量过大。
2. 如果遍历到某条线索，发现正确数量太多，那么及时返回。
3. 枚举某条线索的“未确定的正确数位组合”时，忽略那些目前是错误的或者是已经填数的数位。

本题也可以使用meet-in-the-middle思想，或者是[模拟退火](https://en.wikipedia.org/wiki/Simulated_annealing)算法完成。

## 代码

```C++
# include <bits/stdc++.h>
using namespace std;
const int N = 22;
const int M = 16;
const int D = 10;
int vis[M][D] = {0};
int tmp[M];
int A[N][M] = {
        {2, 3, 2, 1, 3, 8, 6, 1, 0, 4, 3, 0, 3, 8, 4, 5},
        {3, 8, 4, 7, 4, 3, 9, 6, 4, 7, 2, 9, 3, 0, 4, 7},
        {3, 1, 7, 4, 2, 4, 8, 4, 3, 9, 4, 6, 5, 8, 5, 8},
        {8, 1, 5, 7, 3, 5, 6, 3, 4, 4, 1, 1, 8, 4, 8, 3},
        {6, 3, 7, 5, 7, 1, 1, 9, 1, 5, 0, 7, 7, 0, 5, 0},
        {6, 9, 1, 3, 8, 5, 9, 1, 7, 3, 1, 2, 1, 3, 6, 0},
        {4, 8, 9, 5, 7, 2, 2, 6, 5, 2, 1, 9, 0, 3, 0, 6},
        {5, 6, 1, 6, 1, 8, 5, 6, 5, 0, 5, 1, 8, 2, 9, 3},
        {4, 5, 1, 3, 5, 5, 9, 0, 9, 4, 1, 4, 6, 1, 1, 7},
        {2, 6, 1, 5, 2, 5, 0, 7, 4, 4, 3, 8, 6, 8, 9, 9},
        {6, 4, 4, 2, 8, 8, 9, 0, 5, 5, 0, 4, 2, 7, 6, 8},
        {2, 3, 2, 6, 5, 0, 9, 4, 7, 1, 2, 7, 1, 4, 4, 8},
        {5, 2, 5, 1, 5, 8, 3, 3, 7, 9, 6, 4, 4, 3, 2, 2},
        {2, 6, 5, 9, 8, 6, 2, 6, 3, 7, 3, 1, 6, 8, 6, 7},
        {5, 8, 5, 5, 4, 6, 2, 9, 4, 0, 8, 1, 0, 5, 8, 7},
        {9, 7, 4, 2, 8, 5, 5, 5, 0, 7, 0, 6, 8, 3, 5, 3},
        {4, 2, 9, 6, 8, 4, 9, 6, 4, 3, 6, 0, 7, 5, 4, 3},
        {7, 8, 9, 0, 9, 7, 1, 5, 4, 8, 9, 0, 8, 0, 6, 7},
        {8, 6, 9, 0, 0, 9, 5, 8, 5, 1, 5, 2, 6, 2, 5, 4},
        {1, 7, 4, 8, 2, 7, 0, 4, 7, 6, 7, 5, 8, 2, 7, 6},
        {3, 0, 4, 1, 6, 3, 1, 1, 1, 7, 2, 2, 4, 6, 3, 5},
        {1, 8, 4, 1, 2, 3, 6, 4, 5, 4, 3, 2, 4, 5, 8, 9}
};
int B[N] = {0, 1, 1, 1, 1, 1, 1, 2, 2, 2, 2, 2, 2, 2, 3, 3, 3, 3, 3, 3, 3, 3};
bool dfs1(int, int);
bool dfs2(int f, int finish, int f1, int cnt, int st, char *neglect) {
    if (f1 == cnt) {
        for (int i = 0; i < M; i++)
            vis[i][A[f][i]]++;
        if (dfs1(f + 1, finish + cnt)) return true;
        for (int i = 0; i < M; i++)
            vis[i][A[f][i]]--;
        return false;
    }
    for (int i = st; i < M; i++) {
        if (neglect[i]) continue;
        tmp[i] = A[f][i];
        if (dfs2(f, finish, f1 + 1, cnt, i + 1, neglect)) return true;
        tmp[i] = -1;
    }
    return false;
}
bool dfs1(int f, int finish) {
    if (f == N) {
        for (int i = 0; i < M; i++) {
            if (tmp[i] == -1) {
                for (int j = 0; j < D; j++) {
                    if (vis[i][j] == 0)
                        tmp[i] = j;
                }
            }
        }
        return true;
    }
    int cnt = B[f];
    for (int i = 0; i < M; i++)
        cnt -= (A[f][i] == tmp[i]);
    if (cnt < 0)return false;
    char neglect[M] = {0};
    for (int i = 0; i < M; i++)
        if (tmp[i] != -1 || vis[i][A[f][i]]) neglect[i] = 1;
    if (dfs2(f, finish, 0, cnt, 0, neglect)) return true;
    return false;
}
int main() {
    memset(tmp,-1,sizeof(tmp));
    dfs1(0, 0);
    string ans;
    for (int i = 0; i < M; i++)
        ans += char('0' + tmp[i]);
    cout << ans << endl;
    return 0;
}
```
