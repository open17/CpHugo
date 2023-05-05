---
title: 线段树模板
description: 作者：open17
slug: SegmentTree
date: 2023-05-05 00:00:00+0000
image: cover.jpg
categories:
    - DS
tags:
    - templates
    - c++
    - SegmentTree
---
## lazy线段树模板
- 区间修改logn
- 区间查询logn
（维护存在交换律的信息）
```cpp
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
```