---
title: 洛谷0002——最大加权矩形
description: 作者：open17
slug: luogu0002
date: 2023-05-02 00:00:00+0000
categories:
    - Alg
tags:
    - presum
    - c++
    - luogu
---
# 最大加权矩形

## 题目描述

为了更好的备战 NOIP2013，电脑组的几个女孩子 LYQ,ZSC,ZHQ 认为，我们不光需要机房，我们还需要运动，于是就决定找校长申请一块电脑组的课余运动场地，听说她们都是电脑组的高手，校长没有马上答应他们，而是先给她们出了一道数学题，并且告诉她们：你们能获得的运动场地的面积就是你们能找到的这个最大的数字。

校长先给他们一个 $n\times n$ 矩阵。要求矩阵中最大加权矩形，即矩阵的每一个元素都有一权值，权值定义在整数集上。从中找一矩形，矩形大小无限制，是其中包含的所有元素的和最大 。矩阵的每个元素属于 $[-127,127]$ ,例如

```plain
 0 –2 –7  0 
 9  2 –6  2
-4  1 –4  1 
-1  8  0 –2
```

在左下角：

```plain
9  2
-4  1
-1  8
```

和为 $15$。

几个女孩子有点犯难了，于是就找到了电脑组精打细算的 HZH，TZY 小朋友帮忙计算，但是遗憾的是他们的答案都不一样，涉及土地的事情我们可不能含糊，你能帮忙计算出校长所给的矩形中加权和最大的矩形吗？

## 输入格式

第一行：$n$，接下来是 $n$ 行 $n$ 列的矩阵。

## 输出格式

最大矩形（子矩阵）的和。

## 样例 #1

### 样例输入 #1

```
4
0 -2 -7 0
 9 2 -6 2
-4 1 -4  1 
-1 8  0 -2
```

### 样例输出 #1

```
15
```

## 提示

$1 \leq n\le 120$

## code
```cpp
#include<bits/stdc++.h>
using namespace std;
#define ios ios::sync_with_stdio(false);cin.tie(0);cout.tie(0);
#define FOR(w, a, n) for(int w=(a);w<(n);++w)
#define inf 0x3f
typedef long long ll;
typedef pair<int, int> pii;
const int N=123;
int a[N][N];
int b[N][N];
int main() {
    ios
    int n;
    cin>>n;
    FOR(i,0,n){
        FOR(j,0,n){
            cin>>a[i][j];
        }
    }
    FOR(i,1,n+1){
        FOR(j,1,n+1){
            b[i][j]=b[i-1][j]+b[i][j-1]-b[i-1][j-1]+a[i-1][j-1];
        }
    }
    int ans=-inf;
    FOR(x1,1,n+1){
        FOR(y1,1,n+1){
            FOR(x2,x1,n+1){
                FOR(y2,y1,n+1){
                    ans=max(ans,b[x2][y2] - b[x1 - 1][y2] - b[x2][y1 - 1] + b[x1 - 1][y1 - 1]);
                }
            }
        }
    }
    cout << ans << endl;
    return 0;
}

```