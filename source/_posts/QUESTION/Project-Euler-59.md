---
title: Project Euler 59
category:
  - Project Euler
tags:
mathjax: true
date: 2022-04-30 10:31:57
---

<escape><!-- more --></escape>

# Project Euler 59

## 题目

### XOR decryption

Each character on a computer is assigned a unique code and the preferred standard is ASCII (American Standard Code for Information Interchange). For example, uppercase A = $65$, asterisk (*) = $42$, and lowercase k = $107$.

A modern encryption method is to take a text file, convert the bytes to ASCII, then XOR each byte with a given value, taken from a secret key. The advantage with the XOR function is that using the same encryption key on the cipher text, restores the plain text; for example, $65\ \text{XOR}\ 42 = 107$, then $107\ \text{XOR}\ 42 = 65$.

For unbreakable encryption, the key is the same length as the plain text message, and the key is made up of random bytes. The user would keep the encrypted message and the encryption key in different locations, and without both “halves”, it is impossible to decrypt the message.

Unfortunately, this method is impractical for most users, so the modified method is to use a password as a key. If the password is shorter than the message, which is likely, the key is repeated cyclically throughout the message. The balance for this method is using a sufficiently long password key for security, but short enough to be memorable.

Your task has been made easy, as the encryption key consists of three lower case characters. Using [cipher.txt](../resources/p059_cipher.txt) (right click and ‘Save Link/Target As…’), a file containing the encrypted ASCII codes, and the knowledge that the plain text must contain common English words, decrypt the message and find the sum of the ASCII values in the original text.

## 解决方案

在这种加密方式下，把密文的每个字符分成三份，第$i$个字符在第$i\%3$份中，观察统计特性（取前四个最多的）。

```
[(69, 86), (0, 62), (12, 34), (17, 32)]
[(88, 77), (29, 60), (12, 31), (11, 30)]
[(80, 103), (21, 42), (4, 40), (2, 29)]
```

可以发现，某一个单一字符的密文使用的频率异常高，这是因为一篇英文文章中，有非常多数量的空格。可以认为，每一份的密文中，对应的密钥是空格的ACII码和频率最大的密文字符的异或值。

找到密钥后，直接解密即可。

NOTE: 本题所使用的密码学方案，是[维吉尼亚密码](https://en.wikipedia.org/wiki/Vigen%C3%A8re_cipher)的高级版本（维吉尼亚密码的基础版本是做$\mathbb{Z_{26}}$上的模加法运算，而这里是做$\{0,1\}^7$上的异或运算），是一种基于多表密码的古典密码学方案。于19~20世纪被破译。

## 代码

```py
from collections import Counter

M = 3
ls = [int(x) for x in open('p059_cipher.txt', 'r').readlines()[0].split(',')]
counter_list = [Counter(ls[i::3]) for i in range(M)]
# for v in counter_list:
#     print(v.most_common(4))
key = [counter_list[i].most_common(1)[0][0] ^ ord(' ') for i in range(M)]
ans = 0
for i in range(len(ls)):
    ans += key[i % 3] ^ ls[i]
print(ans)
```
