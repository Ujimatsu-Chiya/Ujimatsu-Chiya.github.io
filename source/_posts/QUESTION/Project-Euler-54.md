---
title: Project Euler 54
tags:
  - Project Euler
  - 模拟
mathjax: true
date: 2022-04-30 10:31:35
---

<escape><!-- more --></escape>

# Project Euler 54

## 题目

### Poker hands

In the card game poker, a hand consists of five cards and are ranked, from lowest to highest, in the following way:

- **High Card**: Highest value card.
- **One Pair**: Two cards of the same value.
- **Two Pairs**: Two different pairs.
- **Three of a Kind**: Three cards of the same value.
- **Straight**: All cards are consecutive values.
- **Flush**: All cards of the same suit.
- **Full House**: Three of a kind and a pair.
- **Four of a Kind**: Four cards of the same value.
- **Straight Flush**: All cards are consecutive values of same suit.
- **Royal Flush**: Ten, Jack, Queen, King, Ace, in same suit.

The cards are valued in the order:2, 3, 4, 5, 6, 7, 8, 9, 10, Jack, Queen, King, Ace.

If two players have the same ranked hands then the rank made up of the highest value wins; for example, a pair of eights beats a pair of fives (see example 1 below). But if two ranks tie, for example, both players have a pair of queens, then highest cards in each hand are compared (see example 4 below); if the highest cards tie then the next highest cards are compared, and so on.

Consider the following five hands dealt to two players:

|Hand|Player 1|Player 2|Winner|
|-|-|-|-|
|1|5H 5C 6S 7S KD|2C 3S 8S 8D TD|Player 2|
||Pair of Fives|Pair of Eights||
|2|5D 8C 9S JS AC|2C 5C 7D 8S QH|Player 1|
||Highest card Ace|Highest card Queen||
|3|2D 9C AS AH AC|3D 6D 7D TD QD|Player 2|
||Three Aces|Flush with Diamonds||
|4|4D 6S 9H QH QC|3D 6D 7H QD QS|Player 1|
||Pair of Queens|Pair of Queens||
||Highest card Nine|Highest card Seven||
|5|2H 2D 4C 4D 4S|3C 3D 3S 9S 9D|Player 1|
||Full House|Full House||
||with Three Fours|with Three Threes||

The file, [poker.txt](../resources/p054_poker.txt), contains one-thousand random hands dealt to two players. Each line of the file contains ten cards (separated by a single space): the first five are Player 1’s cards and the last five are Player 2’s cards. You can assume that all hands are valid (no invalid characters or repeated cards), each player’s hand is in no specific order, and in each hand there is a clear winner.

How many hands does Player 1 win?

## 解决方案

本体属于细节题，参考代码和注释。
基本思想是先判断手牌的等级，然后再计算出当前等级下的手牌最大的那张。

## 代码

```py
# 判断5张牌是否同花。
def same_suit(p):
    for i in range(4):
        if p[i][1] != p[i + 1][1]:
            return False
    return True


# 判断5张牌是否一个顺子。
def order(p):
    for i in range(4):
        if ord(p[i + 1][0]) - ord(p[i][0]) != 1:
            return False
    return True


def get_level(p):
    # 将5张牌的牌面收集起来。
    r = p[0][0] + p[1][0] + p[2][0] + p[3][0] + p[4][0]

    if same_suit(p) and order(p):
        # 同花大顺
        if p[4][0] == 'M':
            return p, p[4], 10
        # 同花顺
        else:
            return p, p[4], 9
    # 四条
    elif r[0] == r[1] == r[2] == r[3]:
        return p[0:4], p[3], 8
    elif r[1] == r[2] == r[3] == r[4]:
        return p[1:5], p[4], 8
    # 葫芦
    elif r[0] == r[1] == r[2] and r[3] == r[4] or r[2] == r[3] == r[4] and r[0] == r[1]:
        return p, p[2], 7
    # 同花
    elif same_suit(p):
        return p, p[4], 6
    # 顺子
    elif order(p):
        return p, p[4], 5
    # 三条
    elif r[0] == r[1] == r[2]:
        return p[0:3], p[2], 4
    elif r[3] == r[1] == r[2]:
        return p[1:4], p[2], 4
    elif r[3] == r[4] == r[2]:
        return p[2:5], p[2], 4
    # 两对
    elif r[0] == r[1] and r[2] == r[3]:
        return p[0:4], p[3], 3
    elif r[0] == r[1] and r[3] == r[4]:
        return p[0:2] + p[3:5], p[3], 3
    elif r[1] == r[2] and r[3] == r[4]:
        return p[1:5], p[3], 3
    # 一对
    elif r[0] == r[1]:
        return p[0:2], p[1], 2
    elif r[1] == r[2]:
        return p[1:3], p[1], 2
    elif r[2] == r[3]:
        return p[2:4], p[3], 2
    elif r[3] == r[4]:
        return p[3:5], p[3], 2
    # 单张
    else:
        return [p[4]], p[4], 1


def cmp(p1, p2):
    # 三元组(x, y, z)分别表示：真实用上比较等级的牌；真实用上比较等级的牌中，牌面最大的那张；等级数
    x1, y1, z1 = get_level(p1)
    x2, y2, z2 = get_level(p2)
    # 如果等级不同，直接判断等级。
    if z1 > z2:
        return 1
    elif z1 < z2:
        return 0
    # 如果等级相同，直接由相同数量最多的那张牌进行牌面比较（QQQQA < KKKK2，2244A < 3355K）。
    if y1[0] > y2[0]:
        return 1
    elif y1[0] < y2[0]:
        return 0
    # 否则，就用剩下的牌的最大牌面比大小。
    l1 = list(set(p1) - set(x1))
    l2 = list(set(p2) - set(x2))
    l1.sort()
    l2.sort()
    if l1[-1][0] > l2[-1][0]:
        return 1
    return 0


ls = [s[:-1].split(' ') for s in open('p054_poker.txt', 'r').readlines()]

# 牌面大小重新映射，牌面越大，字母序号越大。
mp = {'2': 'A', '3': 'B', '4': 'C', '5': 'D', '6': 'E', '7': 'F', '8': 'G', '9': 'H', 'T': 'I', 'J': 'J', 'Q': 'K',
      'K': 'L', 'A': 'M'}
ans = 0
for v in ls:
    for i in range(len(v)):
        v[i] = mp[v[i][0]] + v[i][1]
    p1, p2 = v[:5], v[5:]

    # 两个人的手牌先按牌面大小排好序。
    p1.sort()
    p2.sort()
    ans += cmp(p1, p2)
print(ans)
```
