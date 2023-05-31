---
title: 并查集模板
description: 一种擅长于维护具有传递性关系的数据结构
slug: buf
date: 2023-05-05 00:00:00+0000
categories:
    - DS
tags:
    - Templates
    - Buf
---
##  按序合并路径压缩优化并查集
### 封装模板
```cpp
class Buf {
public:
    Buf(int sz) : root(sz), rank(sz) {
        for (int i = 0; i < sz; i++) {
            root[i] = i;
            rank[i] = 1;
        }
    }

    int find(int x) {
        if (x == root[x]) {
            return x;
        }
        return root[x] = find(root[x]);
    }

    void unionSet(int x, int y) {
        int rootX = find(x);
        int rootY = find(y);
        if (rootX != rootY) {
            if (rank[rootX] > rank[rootY]) {
                root[rootY] = rootX;
            } else if (rank[rootX] < rank[rootY]) {
                root[rootX] = rootY;
            } else {
                root[rootY] = rootX;
                rank[rootX] += 1;
            }
        }
    }

    bool connected(int x, int y) {
        return find(x) == find(y);
    }

private:
    vector<int> root;
    vector<int> rank;
};
```
### 非封装模板
```cpp
ll root[MAXN],rank[MAXN],n;
void initbuf(ll n){
    for (ll i = 0; i < n; i++) {
        root[i] = i;
    }
}
ll find(ll x) {
    if (x == root[x]) {
        return x;
    }
    return root[x] = find(root[x]);
}
void unionSet(ll x, ll y) {
    ll rootX = find(x);
    ll rootY = find(y);
    if (rootX != rootY) {
        if (rank[rootX] > rank[rootY]) root[rootY] = rootX;
        else if (rank[rootX] < rank[rootY])root[rootX] = rootY;
        else {
            root[rootY] = rootX;
            rank[rootX] += 1;
        }
    }
}
bool connected(ll x, ll y) {
    return find(x) == find(y);
}
```