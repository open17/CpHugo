---
title: 前缀和与差分模板
description: 作者：open17
slug: preSum
date: 2023-05-02 00:00:00+0000
categories:
    - Alg
tags:
    - templates
    - presum
    - c++
---
## 一维前缀和
```cpp
// S[i] = a[1] + a[2] + ... a[i]
// a[l] + ... + a[r] = S[r] - S[l - 1]
S[r] - S[l - 1]
```
## 二维前缀和
```cpp
// S[i, j] = 第i行j列格子左上部分所有元素的和
b[i][j]=b[i-1][j]+b[i][j-1]-b[i-1][j-1]+a[i][j]
// 以(x1, y1)为左上角，(x2, y2)为右下角的子矩阵的和为：
b[x2][y2] - b[x1 - 1][y2] - b[x2][y1 - 1] + b[x1 - 1][y1 - 1]
```
## 一维差分
```cpp
// 给区间[l, r]中的每个数加上c：
B[l] += c, B[r + 1] -= c
```
## 二维差分
```cpp
// 给以(x1, y1)为左上角，(x2, y2)为右下角的子矩阵中的所有元素加上c：
S[x1][y1] += c, S[x2 + 1][y1] -= c, S[x1][y2 + 1] -= c, S[x2 + 1][y2 + 1] += c
```
## tips
- 从1开始，0开大，防特判