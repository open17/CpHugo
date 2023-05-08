---
title: 洛谷0005——【模板】线段树 1
description: 板子题
slug: luogu0005
date: 2023-05-05 00:00:00+0000
categories:
    - Alg
tags:
    - luogu
    - c++
    - SegmentTree
---
# 【模板】线段树 1

## 题目描述

如题，已知一个数列，你需要进行下面两种操作：

1. 将某区间每一个数加上 $k$。
2. 求出某区间每一个数的和。

## 输入格式

第一行包含两个整数 $n, m$，分别表示该数列数字的个数和操作的总个数。

第二行包含 $n$ 个用空格分隔的整数，其中第 $i$ 个数字表示数列第 $i$ 项的初始值。

接下来 $m$ 行每行包含 $3$ 或 $4$ 个整数，表示一个操作，具体如下：

1. `1 x y k`：将区间 $[x, y]$ 内每个数加上 $k$。
2. `2 x y`：输出区间 $[x, y]$ 内每个数的和。

## 输出格式

输出包含若干行整数，即为所有操作 2 的结果。

## 样例 #1

### 样例输入 #1

```
5 5
1 5 4 2 3
2 2 4
1 2 3 2
2 3 4
1 1 5 1
2 1 4
```

### 样例输出 #1

```
11
8
20
```

## 提示

对于 $30\%$ 的数据：$n \le 8$，$m \le 10$。  
对于 $70\%$ 的数据：$n \le {10}^3$，$m \le {10}^4$。  
对于 $100\%$ 的数据：$1 \le n, m \le {10}^5$。

保证任意时刻数列中所有元素的绝对值之和 $\le {10}^{18}$。

**【样例解释】**

![](https://cdn.luogu.com.cn/upload/pic/2251.png)


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
    tree[p << 1] += mark[p] * (len - len / 2);
    mark[p << 1] += mark[p];
    tree[p << 1 | 1] += mark[p] * (len / 2);
    mark[p << 1 | 1] += mark[p];
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
        tree[p] += d * (cr - cl + 1);
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
    FOR(i,1,n+1){
        cin>>A[i];
    }
    build();
    int op,x,y,k;
    while(m--){
        cin>>op;
        if(op==1){
            cin>>x>>y>>k;
            update(x,y,k);
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