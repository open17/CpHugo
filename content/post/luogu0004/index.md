---
title: 洛谷0004——[TJOI2009] 开关
description: 略微修改的板子题，不过前提是要彻底理解相关板子
slug: luogu0004
date: 2023-05-05 00:00:00+0000
categories:
    - DS
tags:
    - Segment Tree
    - Luogu
---
# [TJOI2009] 开关

## 题目描述

现有 $n$ 盏灯排成一排，从左到右依次编号为：$1$，$2$，……，$n$。然后依次执行 $m$ 项操作。

操作分为两种：

1. 指定一个区间 $[a,b]$，然后改变编号在这个区间内的灯的状态（把开着的灯关上，关着的灯打开）；
2. 指定一个区间 $[a,b]$，要求你输出这个区间内有多少盏灯是打开的。

**灯在初始时都是关着的。**

## 输入格式

第一行有两个整数 $n$ 和 $m$，分别表示灯的数目和操作的数目。

接下来有 $m$ 行，每行有三个整数，依次为：$c$、$a$、$b$。其中 $c$ 表示操作的种类。

- 当 $c$ 的值为 $0$ 时，表示是第一种操作。
- 当 $c$ 的值为 $1$ 时，表示是第二种操作。

$a$ 和 $b$ 则分别表示了操作区间的左右边界。

## 输出格式

每当遇到第二种操作时，输出一行，包含一个整数，表示此时在查询的区间中打开的灯的数目。

## 样例 #1

### 样例输入 #1

```
4 5
0 1 2
0 2 4
1 2 3
0 2 4
1 1 4
```

### 样例输出 #1

```
1
2
```

## 提示

#### 数据规模与约定

对于全部的测试点，保证 $2\le n\le 10^5$，$1\le m\le 10^5$，$1\le a,b\le n$，$c\in\{0,1\}$。\

## code
```cpp
#include<bits/stdc++.h>
using namespace std;
#define ios ios::sync_with_stdio(false);cin.tie(0);cout.tie(0);
#define FOR(w, a, n) for(int w=(a);w<(n);++w)
#define inf 0x3f
typedef long long ll;
typedef pair<int, int> pii;
const int MAXN=1e5+9;
//开4倍
//n 为维护的数组长度，A为维护的数组
ll tree[MAXN << 2], mark[MAXN << 2], n,A[MAXN];
void push_down(int p, int len)
{
    //叶子节点可以不更新
    if (len <= 1) return;
    //向下传递lazy标记
    if(mark[p]%2)tree[p << 1] = (len - len / 2)-tree[p<<1];
    mark[p << 1] += mark[p]%2;
    if(mark[p]%2)tree[p << 1 | 1] = (len / 2)-tree[p<<1|1];
    mark[p << 1 | 1] += mark[p]%2;
    //向下传递了，自然清除自身的tag
    mark[p] = 0;
}
void push_up(int p){
    //这里维护的是区间和
    tree[p] = tree[p << 1] + tree[p << 1 | 1];
}
void build(int p = 1, int cl = 1, int cr = n)
{
    //如果叶子节点
    if (cl == cr) return void(tree[p] = A[cl]);
    //左右递归建树
    int mid = (cl + cr) >> 1;
    build(p << 1, cl, mid);
    build(p << 1 | 1, mid + 1, cr);
    push_up(p);
}
ll query(int l, int r, int p = 1, int cl = 1, int cr = n)
{
    //当前被包含
    if (cl >= l && cr <= r) return tree[p];
    push_down(p, cr - cl + 1);
    ll mid = (cl + cr) >> 1, ans = 0;
    if (mid >= l) ans += query(l, r, p << 1, cl, mid);
    if (mid < r) ans += query(l, r, p << 1 | 1, mid + 1, cr);
    return ans;
}
void update(int l, int r, int d, int p = 1, int cl = 1, int cr = n)
{
    //当前被包含
    if (cl >= l && cr <= r){
        tree[p] = d * (cr - cl + 1)-tree[p];
        mark[p] += d;
        return;
    }
    push_down(p, cr - cl + 1);
    int mid = (cl + cr) >> 1;
    if (mid >= l) update(l, r, d, p << 1, cl, mid);
    if (mid < r) update(l, r, d, p << 1 | 1, mid + 1, cr);
    push_up(p);
}
int main() {
    ios
    int m;
    cin>>n>>m;
    build();
    int op,x,y;
    while(m--){
        cin>>op;
        if(op==0){
            cin>>x>>y;
            update(x,y,1);
        }
        else{
            cin>>x>>y;
            ll res=query(x,y);
            cout<<res<<endl;
        }
    }
    return 0;
}
```
