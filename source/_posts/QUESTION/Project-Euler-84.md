---
title: Project Euler 84
category:
  - Project Euler
tags:
  - 模拟
  - 概率
mathjax: true
date: 2022-05-03 09:22:32
---

<escape><!-- more --></escape>

# Project Euler 84

## 题目

### Monopoly odds

In the game, *Monopoly*, the standard board is set up in the following way:

![](../images/p084_monopoly_board.png)

A player starts on the GO square and adds the scores on two 6-sided dice to determine the number of squares they advance in a clockwise direction. Without any further rules we would expect to visit each square with equal probability: $2.5\%$. However, landing on G2J (Go To Jail), CC (community chest), and CH (chance) changes this distribution.

In addition to G2J, and one card from each of CC and CH, that orders the player to go directly to jail, if a player rolls three consecutive doubles, they do not advance the result of their 3rd roll. Instead they proceed directly to jail.

At the beginning of the game, the CC and CH cards are shuffled. When a player lands on CC or CH they take a card from the top of the respective pile and, after following the instructions, it is returned to the bottom of the pile. There are sixteen cards in each pile, but for the purpose of this problem we are only concerned with cards that order a movement; any instruction not concerned with movement will be ignored and the player will remain on the CC/CH square.

- Community Chest ($2/16$ cards):
    1. Advance to GO
    2. Go to JAIL

- Chance (10/16 cards):
    1. Advance to GO
    2. Go to JAIL
    3. Go to C1
    4. Go to E3
    5. Go to H2
    6. Go to R1
    7. Go to next R (railway company)
    8. Go to next R
    9. Go to next U (utility company)
    10. Go back 3 squares.

The heart of this problem concerns the likelihood of visiting a particular square. That is, the probability of finishing at that square after a roll. For this reason it should be clear that, with the exception of G2J for which the probability of finishing on it is zero, the CH squares will have the lowest probabilities, as 5/8 request a movement to another square, and it is the final square that the player finishes at on each roll that we are interested in. We shall make no distinction between "Just Visiting" and being sent to JAIL, and we shall also ignore the rule about requiring a double to "get out of jail", assuming that they pay to get out on their next turn.

By starting at GO and numbering the squares sequentially from 00 to 39 we can concatenate these two-digit numbers to produce strings that correspond with sets of squares.

Statistically it can be shown that the three most popular squares, in order, are JAIL $(6.24\%)$ = Square 10, E3 $(3.18\%)$ = Square 24, and GO $(3.09\%)$ = Square 00. So these three most popular squares can be listed with the six-digit modal string: $102400$.

If, instead of using two $6$-sided dice, two $4$-sided dice are used, find the six-digit modal string.

## 解决方案

第一种方法直接通过随机数进行模拟整个游戏过程，模拟的过程中需要注意细节。

第二种方法则是基于[马尔科夫链](https://en.wikipedia.org/wiki/Markov_chain)，计算出[极限分布](https://en.wikipedia.org/wiki/Markov_chain#Stationary_distribution_relation_to_eigenvectors_and_simplices)。

本题需要一个假设：虽然CC卡和CH卡一开始就是打乱的，但是在游戏过程中，每次抽取卡片的过程却是依赖上一次的抽卡结果（每次抽取的都是最上面的那一张）。为简化，这里将假设游戏过程中的抽卡也是随机的。

由此，将整个马尔科夫链简化成了$40\times 3=120$个状态（$40$个位置，$3$次相同点数的次数）。

只要构造出概率转移矩阵，就能够计算出极限分布（即分别在每个格子上的概率）。

（基于马尔科夫链的做法和代码待补充）

## 代码

```py
from random import randint, shuffle

T = 10 ** 7
M = 4


def get_list():
    ls = [x for x in range(1, 17)]
    shuffle(ls)
    return ls


def get_dices():
    a, b = randint(1, M), randint(1, M)
    return a + b, a == b

# 根据地点计算下一个R。
def next_rail(pos: int):
    if 5 <= pos < 15:
        return 15
    elif 15 <= pos < 25:
        return 25
    elif 25 <= pos < 35:
        return 35
    else:
        return 5

# 根据地点计算下一个U。
def next_utility(pos: int):
    if 12 <= pos < 28:
        return 28
    else:
        return 12


cards = [-1, 0, 10, 11, 24, 39, 5]


def cc(id: int, pos: int):
    # 移动到指定地点的卡
    if id <= 2:
        return cards[id]
    else:
        return pos


def ch(id: int, pos: int):
    # 移动到指定地点的卡
    if id <= 6:
        return cards[id]
    # 2张下一个R卡
    elif 7 <= id <= 8:
        return next_rail(pos)
    # 1张下一个U卡
    elif id == 9:
        return next_utility(pos)
    # 后退三格卡
    elif id == 10:
        pos -= 3
        if pos < 0:
            pos += 40
        return pos
    else:
        return pos


cnt = [0 for i in range(40)]
# cc卡和ch卡分别用1~16的标号进行表示。
ch_card = get_list()
cc_card = get_list()
pos = dbc = 0
for i in range(T):
    w, f = get_dices()
    if f:
        dbc += 1
    else:
        dbc = 0
    if dbc == 3:
        pos = 10
        dbc = 0
    else:
        pos += w
        if pos >= 40:
            pos -= 40
            # 获取的是CC卡
        if pos in [2, 17, 33]:
            tp = cc_card.pop()
            cc_card.insert(0, tp)
            pos = cc(tp, pos)
            # 获得的是CH卡
        elif pos in [7, 22, 36]:
            tp = ch_card.pop()
            ch_card.insert(0, tp)
            pos = ch(tp, pos)
        elif pos == 30:
            pos = 10
        # 无论什么原因，只要到达监狱，次数就清零。
        if pos == 10:
            dbc = 0
    cnt[pos] += 1
a = [[i, cnt[i]] for i in range(40)]
a.sort(key=lambda t: t[1])
ans = str(a[-1][0]) + str(a[-2][0]) + str(a[-3][0])
print(ans)

```
