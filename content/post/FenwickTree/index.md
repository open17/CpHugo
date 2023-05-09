---
title: 树状数组模板
description: 一种简单的用于维护区间信息的数据结构
slug: FenwickTree
date: 2023-05-05 00:00:00+0000
image: https://img2.baidu.com/it/u=1929941019,3324507395&fm=253&fmt=auto&app=138&f=JPEG?w=889&h=500
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