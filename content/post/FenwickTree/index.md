---
title: 树状数组模板
description: 作者：open17
slug: FenwickTree
date: 2023-05-05 00:00:00+0000
image: cover.jpg
categories:
    - DS
tags:
    - templates
    - c++
    - FenwickTree
---
## 封装模板
```cpp
class FenwickTree{
public:
    int n;
    vector<int> tree;
    FenwickTree(int i): n(i),tree(i+1){
        for(int a=0;a<=i;a++){
            tree[a]=0;
        }
    }
    void update(int i,int val){
        while(i<=n){
            tree[i]+=val;
            i+=i&(-i);
        }
    }
    int query(int i){
        int res=0;
        while(i>0){
            res+=tree[i];
            i-=i&(-i);
        }
        return res;
    }
}
```
## 非封装模板
```cpp
//n为实际长度
ll tree[MAXN],n;
void update(int i,int val){
    while(i<=n){
        tree[i]+=val;
        i+=i&(-i);
    }
}
int query(int i){
    int res=0;
    while(i>0){
        res+=tree[i];
        i-=i&(-i);
    }
    return res;
}
```