---
title: 洛谷0003——并查集
description: 作者：open17
slug: luogu0003
date: 2023-05-05 00:00:00+0000
image: cover.jpg
categories:
    - DS
tags:
    - buf
    - c++
    - luogu
---
# 【模板】并查集

## 题目描述

如题，现在有一个并查集，你需要完成合并和查询操作。

## 输入格式

第一行包含两个整数 $N,M$ ,表示共有 $N$ 个元素和 $M$ 个操作。

接下来 $M$ 行，每行包含三个整数 $Z_i,X_i,Y_i$ 。

当 $Z_i=1$ 时，将 $X_i$ 与 $Y_i$ 所在的集合合并。

当 $Z_i=2$ 时，输出 $X_i$ 与 $Y_i$ 是否在同一集合内，是的输出 
 `Y` ；否则输出 `N` 。

## 输出格式

对于每一个 $Z_i=2$ 的操作，都有一行输出，每行包含一个大写字母，为 `Y` 或者 `N` 。

## 样例 #1

### 样例输入 #1

```
4 7
2 1 2
1 1 2
2 1 2
1 3 4
2 1 4
1 2 3
2 1 4
```

### 样例输出 #1

```
N
Y
N
Y
```

## 提示

对于 $30\%$ 的数据，$N \le 10$，$M \le 20$。

对于 $70\%$ 的数据，$N \le 100$，$M \le 10^3$。

对于 $100\%$ 的数据，$1\le N \le 10^4$，$1\le M \le 2\times 10^5$，$1 \le X_i, Y_i \le N$，$Z_i \in \{ 1, 2 \}$。


## code
```cpp
#include<bits/stdc++.h>
using namespace std;
#define ios ios::sync_with_stdio(false);cin.tie(0);cout.tie(0);
#define FOR(w, a, n) for(int w=(a);w<(n);++w)
#define inf 0x3f
typedef long long ll;
typedef pair<int, int> pii;
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
int main() {
    ios
    int n,m,y,x,z;
    cin>>n>>m;
    Buf a=Buf(n+1);
    while(m--){
        cin>>z>>x>>y;
        if(z==1){
            a.unionSet(x,y);
        }
        else{
            if(a.connected(x,y))cout<<"Y";
            else cout<<"N";
            cout<<endl;
        }
    }
    return 0;
}

```