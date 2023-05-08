---
title: 洛谷0001——求区间和
description: 作者：open17
slug: luogu0001
date: 2023-05-02 00:00:00+0000
categories:
    - Alg
tags:
    - presum
    - c++
    - luogu
---
# 【深进1.例1】求区间和

## 题目描述

给定 $n$ 个正整数组成的数列 $a_1, a_2, \cdots, a_n$ 和 $m$ 个区间 $[l_i,r_i]$，分别求这 $m$ 个区间的区间和。对于所有测试数据，$n,m\le10^5,a_i\le 10^4$

## 输入格式

共 $n+m+2$ 行。

第一行，为一个正整数 $n$ 。

第二行，为 $n$ 个正整数 $a_1,a_2, \cdots ,a_n$

第三行，为一个正整数 $m$ 。

第 $4$ 到第 $n+m+2$ 行，每行为两个正整数 $l_i,r_i$ ，满足$1\le l_i\le r_i\le n$

## 输出格式

共 $m$ 行。

第 $i$ 行为第 $i$ 组答案的询问。

## 样例 #1

### 样例输入 #1

```
4
4 3 2 1
2
1 4
2 3
```

### 样例输出 #1

```
10
5
```

## 提示

样例解释：第 1 到第 4 个数加起来和为 10。第 2 个数到第 3 个数加起来和为5。

对于 50% 的数据：$n,m\le 1000$ ；

对于100% 的数据：$n.m\le 10^5,a_i\le 10^4$

## code
```cpp
#include<bits/stdc++.h>
using namespace std;
#define ios ios::sync_with_stdio(false);cin.tie(0);cout.tie(0);
#define FOR(w, a, n) for(int w=(a);w<(n);++w)
#define inf 0x3f
typedef long long ll;
typedef pair<int, int> pii;
const int N=1e5+3;
int a[N];
int b[N];
int main() {
    ios
    int n,m;
    cin>>n;
    FOR(i,0,n){
        cin>>a[i];
    }
    FOR(i,1,n+1){
        b[i]=b[i-1]+a[i-1];
    }
    cin>>m;
    int l,r;
    
    FOR(i,0,m){
        cin>>l>>r;
        cout<<b[r]-b[l-1]<<endl;
    }
    return 0;
}
```