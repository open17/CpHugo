---
title: 倍增LCA模板
description: 运用倍增思想优化的LCA模板
slug: LCA
date: 2023-05-08 00:00:00+0000
categories:
    - Alg
tags:
    - templates
    - c++
    - LCA
    - luogu
---
## 模板
```cpp
// 深度优先搜索，用于求每个节点的深度和祖先信息
void dfs(int u, int fa)
{
    depth[u] = depth[fa] + 1;  // 当前节点的深度为父节点的深度加一
    p[u][0] = fa;  // 当前节点的 2^0 级祖先为父节点
    // 递推求出当前节点的 2^i 级祖先
    for (int i = 1; i < M; i ++ )
        p[u][i] = p[p[u][i - 1]][i - 1];
    // 遍历当前节点的每一个儿子，递归调用 dfs 函数
    for (auto v : g[u])
        if (v != fa)  // 避免向父节点递归
            dfs(v, u);
}

// 求两个节点的最近公共祖先
int lca(int a, int b)
{
    if (depth[a] < depth[b]) swap(a, b);  // 保证 a 深度不小于 b
    // 先将 a 跳到和 b 同一深度
    for (int i = M - 1; i >= 0; i -- )
        if (depth[p[a][i]] >= depth[b])
            a = p[a][i];
    if (a == b) return a;  // 特判 a 和 b 在同一条链上的情况
    // 一起向上跳，直到 a 和 b 的第一个不同的祖先
    for (int i = M - 1; i >= 0; i -- )
        if (p[a][i] != p[b][i])
        {
            a = p[a][i];
            b = p[b][i];
        }
    return p[a][0];  // 返回 a 的父节点，即为 LCA
}

```
# 【模板】最近公共祖先（LCA）

## 题目描述

如题，给定一棵有根多叉树，请求出指定两个点直接最近的公共祖先。

## 输入格式

第一行包含三个正整数 $N,M,S$，分别表示树的结点个数、询问的个数和树根结点的序号。

接下来 $N-1$ 行每行包含两个正整数 $x, y$，表示 $x$ 结点和 $y$ 结点之间有一条直接连接的边（数据保证可以构成树）。

接下来 $M$ 行每行包含两个正整数 $a, b$，表示询问 $a$ 结点和 $b$ 结点的最近公共祖先。

## 输出格式

输出包含 $M$ 行，每行包含一个正整数，依次为每一个询问的结果。

## 样例 #1

### 样例输入 #1

```
5 5 4
3 1
2 4
5 1
1 4
2 4
3 2
3 5
1 2
4 5
```

### 样例输出 #1

```
4
4
1
4
4
```

## 提示

对于 $30\%$ 的数据，$N\leq 10$，$M\leq 10$。

对于 $70\%$ 的数据，$N\leq 10000$，$M\leq 10000$。

对于 $100\%$ 的数据，$1 \leq N,M\leq 500000$，$1 \leq x, y,a ,b \leq N$，**不保证** $a \neq b$。


样例说明：

该树结构如下：

 ![](https://cdn.luogu.com.cn/upload/pic/2282.png) 

第一次询问：$2, 4$ 的最近公共祖先，故为 $4$。

第二次询问：$3, 2$ 的最近公共祖先，故为 $4$。

第三次询问：$3, 5$ 的最近公共祖先，故为 $1$。

第四次询问：$1, 2$ 的最近公共祖先，故为 $4$。

第五次询问：$4, 5$ 的最近公共祖先，故为 $4$。

故输出依次为 $4, 4, 1, 4, 4$。
## code
```cpp
#include <iostream>
#include <cstring>
#include <vector>
#include <cmath>

using namespace std;

const int N = 500010, M = 20;

int n, m, s;  // n：节点数，m：查询次数，s：根节点编号
int depth[N], p[N][M];  // depth：每个节点的深度，p：每个节点的 2^i 级祖先
vector<int> g[N];  // g：树的邻接表表示

// 深度优先搜索，用于求每个节点的深度和祖先信息
void dfs(int u, int fa)
{
    depth[u] = depth[fa] + 1;  // 当前节点的深度为父节点的深度加一
    p[u][0] = fa;  // 当前节点的 2^0 级祖先为父节点
    // 递推求出当前节点的 2^i 级祖先
    for (int i = 1; i < M; i ++ )
        p[u][i] = p[p[u][i - 1]][i - 1];
    // 遍历当前节点的每一个儿子，递归调用 dfs 函数
    for (auto v : g[u])
        if (v != fa)  // 避免向父节点递归
            dfs(v, u);
}

// 求两个节点的最近公共祖先
int lca(int a, int b)
{
    if (depth[a] < depth[b]) swap(a, b);  // 保证 a 深度不小于 b
    // 先将 a 跳到和 b 同一深度
    for (int i = M - 1; i >= 0; i -- )
        if (depth[p[a][i]] >= depth[b])
            a = p[a][i];
    if (a == b) return a;  // 特判 a 和 b 在同一条链上的情况
    // 一起向上跳，直到 a 和 b 的第一个不同的祖先
    for (int i = M - 1; i >= 0; i -- )
        if (p[a][i] != p[b][i])
        {
            a = p[a][i];
            b = p[b][i];
        }
    return p[a][0];  // 返回 a 的父节点，即为 LCA
}

int main()
{
    cin >> n >> m >> s;  // 读入节点数、查询次数和根节点编号
    // 逐个读入每条边，构建树的邻接表表示
    for (int i = 1; i < n; i ++ )
    {
        int a, b;
        cin >> a >> b;
        g[a].push_back(b);
        g[b].push_back(a);
    }
    dfs(s, 0);  // 求每个节点的深度和祖先信息
    while (m -- )
    {
        int a, b;
        cin >> a >> b;  // 读入查询
        cout << lca(a, b) << endl;  // 输出
    }
    return 0;
}
```