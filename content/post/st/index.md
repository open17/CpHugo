---
title: ST表模板
description: 作者：open17
slug: st
date: 2023-05-08 00:00:00+0000
categories:
    - Alg
tags:
    - templates
    - c++
    - st
    - luogu
    - RMQ
---
## 模板
```cpp
const int MAXN = 1e5 + 5;   // 最大数组长度
const int MAXK = 25;        // log2(MAXN) 向上取整

int a[MAXN];                // 输入数组
int st[MAXN][MAXK + 1];     // ST表
int Log2[MAXN];
void build(int n) {
    for (int i = 1; i <= n; i++) {
        st[i][0] = a[i];    // 初始化第一列
    }
    for (int j = 1; j <= MAXK; j++) {
        for (int i = 1; i + (1 << j) - 1 <= n; i++) {
            st[i][j] = min(st[i][j - 1], st[i + (1 << (j - 1))][j - 1]); // 更新ST表
        }
    }
    for (int i = 2; i <= n; ++i) Log2[i] = Log2[i / 2] + 1;
}

int query(int l, int r) {
    int k = Log2[r - l + 1]; // 计算区间长度的对数，向下取整
    return min(st[l][k], st[r - (1 << k) + 1][k]); // 返回区间最小值
}

```
# 【模板】ST 表

## 题目背景

这是一道 ST 表经典题——静态区间最大值

**请注意最大数据时限只有 0.8s，数据强度不低，请务必保证你的每次查询复杂度为 $O(1)$。若使用更高时间复杂度算法不保证能通过。**

如果您认为您的代码时间复杂度正确但是 TLE，可以尝试使用快速读入：

```cpp
inline int read()
{
	int x=0,f=1;char ch=getchar();
	while (ch<'0'||ch>'9'){if (ch=='-') f=-1;ch=getchar();}
	while (ch>='0'&&ch<='9'){x=x*10+ch-48;ch=getchar();}
	return x*f;
}
```

函数返回值为读入的第一个整数。

**快速读入作用仅为加快读入，并非强制使用。**

## 题目描述

给定一个长度为 $N$ 的数列，和 $ M $ 次询问，求出每一次询问的区间内数字的最大值。

## 输入格式

第一行包含两个整数 $N,M$，分别表示数列的长度和询问的个数。

第二行包含 $N$ 个整数（记为 $a_i$），依次表示数列的第 $i$ 项。

接下来 $M$ 行，每行包含两个整数 $l_i,r_i$，表示查询的区间为 $[l_i,r_i]$。

## 输出格式

输出包含 $M$ 行，每行一个整数，依次表示每一次询问的结果。

## 样例 #1

### 样例输入 #1

```
8 8
9 3 1 7 5 6 0 8
1 6
1 5
2 7
2 6
1 8
4 8
3 7
1 8
```

### 样例输出 #1

```
9
9
7
7
9
8
7
9
```

## 提示

对于 $30\%$ 的数据，满足 $1\le N,M\le 10$。

对于 $70\%$ 的数据，满足 $1\le N,M\le {10}^5$。

对于 $100\%$ 的数据，满足 $1\le N\le {10}^5$，$1\le M\le 2\times{10}^6$，$a_i\in[0,{10}^9]$，$1\le l_i\le r_i\le N$。
## code
```cpp
#include <iostream>
#include <string>
#include <vector>

using namespace std;

const int MAXN = 1e5 + 5;   // 最大数组长度
const int MAXK = 25;        // log2(MAXN) 向上取整

int a[MAXN];                // 输入数组
int st[MAXN][MAXK + 1];     // ST表
int Log2[MAXN];
void build(int n) {
    for (int i = 1; i <= n; i++) {
        st[i][0] = a[i];    // 初始化第一列
    }
    for (int j = 1; j <= MAXK; j++) {
        for (int i = 1; i + (1 << j) - 1 <= n; i++) {
            st[i][j] = max(st[i][j - 1], st[i + (1 << (j - 1))][j - 1]); // 更新ST表
        }
    }
    for (int i = 2; i <= n; ++i) Log2[i] = Log2[i / 2] + 1;
}

int query(int l, int r) {
    int k = Log2[r - l + 1]; // 计算区间长度的对数，向下取整
    return max(st[l][k], st[r - (1 << k) + 1][k]); // 返回区间最小值
}

inline int read()
{
	int x=0,f=1;char ch=getchar();
	while (ch<'0'||ch>'9'){if (ch=='-') f=-1;ch=getchar();}
	while (ch>='0'&&ch<='9'){x=x*10+ch-48;ch=getchar();}
	return x*f;
}

int main() {
    int n,m;
    n=read();
    m=read();
    for(int i=1;i<=n;i++){
        a[i]=read();
    }
    build(n);
    while(m--){
        int l=read(),r=read();
        printf("%d\n",query(l,r));
    }
    return 0;
}
```