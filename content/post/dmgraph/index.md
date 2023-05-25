---
title: 离散数学————Graph
description: 基础图论
slug: dmgraph
date: 2023-05-01 00:00:00+0000
categories:
    - Math
    - Graph
tags:
    - Distcrete Structures
---
## Graph Theory
### Graph concepts
#### Definition1
A graph G = (V,E) is a pair and consists of two sets V and such that:  
- V is the set of vertices(顶点)
- E is the set of edges(边)
#### Remember
1. V cannot be empty,but E can(endpoint/node)
2. Each edge have 1 or 2 vertices(1 is a ring)
#### Definition2
- (u,v) is an edge connetcing vettices u and v
- u and v are neighbors (adjacent).
- (u,v) connects  u and v  ((u,v) is incident on u and v).

#### Simple graphs
- each edge connects two different vertices and
- where no two edges connect the same pair of vertices.

#### Multigraph
- A multigraph is a graph that may have multiple edges connecting the same pair of vertices.  
- If there are m different edges associated to the same unordered pair of vertices u and v, (u, v) is an edge of multiplicity.

#### Loops(自环)
- A loop is an edge that connects one vertex to itself.
- Graphs that may include loops, and possibly multiples edges connecting the same pair of vertices are called ***pseudo-graphs***.

#### Directed Graph(有向图)
A directed graph (V,E) consists of a nonempty set V and a
set of directed edges E
#### tips
The edge (u,v) in a directed graph starts at u and ends at v.
#### Degree(度)
The degree of a vertex in an undirected graph is the number of edges connected with it except that a loop at a vertex(自环算2)contribute twice to the degree of that vertex.
##### In-Degree and Out-Degree(入度、出度)
$In:def^-(v)$  
$Out:def^+(v)$
### Handshaking Theorem
For an undirected graph  G= (V,E):   
$$2|E|=\sum_{v \in V}deg(v)$$
### Odd Degree Theorem
In a directed graph G = (V,E)
$$|E|=\sum_{v \in V}deg^-(v)=\sum_{v \in V}deg^+(v)$$

### Special graphs
#### Complete graphs(完全图)
A complete graph is a simple graph in which there is an edge between each pair of distinct vertices, denoted by $K_n$ where n is the number of nodes in the graph
#### Cycles
A cycle is a graph that contains  (n ≥ 3) vertices {V1, V2, …  ,Vn } and n edges (V1, V2), (V2, V3), …, (Vn, V1), denoted by $C_n$ where  is the number of nodes in the graph.
#### Wheels
$Cn$加上中间一个点以及连边，记做$W_n$
#### Cubes
A cube of dimension  n($Q_n$)is a simple graph of $2^n$ vertices, where each vertex represents a bit string of length n. Two vertices are adjacent if and only if they differ by one bit.
#### Bipartite Graphs(二分图)
- A simple graph G = (V,E ) is called bipartite if its vertex set V can be partitioned into two disjoint set V1 and V2 such that every edge in the graph connects a vertex in V1 and a vertex in V2.
- V1 and V2 are called a bipartite of the vertex set V of G
#### Theorem(染色法)
前置知识：二分图不存在奇数环   
A simple graph  G= (V,E) is bipartite if and only if it is
possible to color each vertex with one of two colors so that no
adjacent vertices have the same color. 
```cpp
int n;      // n表示点数
int h[N], e[M], ne[M], idx;     // 邻接表存储图
int color[N];       // 表示每个点的颜色，-1表示未染色，0表示白色，1表示黑色

// 参数：u表示当前节点，c表示当前点的颜色
bool dfs(int u, int c)
{
    color[u] = c;
    for (int i = h[u]; i != -1; i = ne[i])
    {
        int j = e[i];
        if (color[j] == -1)
        {
            if (!dfs(j, !c)) return false;
        }
        else if (color[j] == c) return false;
    }

    return true;
}

bool check()
{
    memset(color, -1, sizeof color);
    bool flag = true;
    for (int i = 1; i <= n; i ++ )
        if (color[i] == -1)
            if (!dfs(i, 0))
            {
                flag = false;
                break;
            }
    return flag;
}

//source：https://www.acwing.com/blog/content/405/
```
#### Complete Bipartite Graphs(完全二分图)
$K_{m,n} $   
In a complete bipartite graph, for any vertex in a subset,there is an edge between it and each vertex in another set.
#### Outline
![图片](http://ask.qcloudimg.com/http-save/yehe-8904777/6fb1fc6209cd5933717fbc5da940c425.png?imageView2/2/w/1200)
### Subgraphs and Proper Subgraphs
- A subgraph H = (W,F) of graph G = (V,E) is made up of vertices W ⊆ V and edges F ⊆ E.
- A subgraph H of G is a proper subgraph if H ≠ G.
### Union of Simple Graphs
The union of two simple graphs G1 = (V1, E1) and G2 = (V2, E2) is the simple graph G = (V, E) such that V = V1 ∪ V2 and E = E1 ∪ E2
### Representing Graphs
- Adjacency matrix(邻接矩阵):dense graph
- Adjacency table(邻接表):sparse graph
### Graph Isomorphism(同构图)
判断同构：推荐使用邻接矩阵判断
### Graph Connectivity 
#### Path
path of length m from vertexu  to vertex v is a sequence of edges e1, e2, … , $e_n$ such that e1 starts at u and $e_n$ ends at v.
#### Circuit
A circuit is a path that begins and ends at the same vertex in graph.
#### Simple path or circuit
A simple path or circuit does not pass through the same edge twice or more.
### Graph Connectedness
- An undirected graph is connected if there is a path between every pair of distinct vertices
- A directed graph is **strongly connected** if there is a path from a to b and from b to a whenever a and b are vertices in the graph
### Euler Paths
- An Euler path in G is a *simple* path containing every edge of G
- An Euler circuit in a graph G is a *simple* circuit containing every edge of G
#### THEOREM
A connected multi-graph has an Euler circuit if and only if each vertex has even degree.
### Hamilton Circuits
- A Hamilton path is a path that traverses each vertex in G exactly once
- A Hamilton circuit is a circuit that traverses each vertex in G exactly once.
#### Ore’s theorem
If for every pair of nonadjacent vertices u and v in the simple graph G with n vertices, deg(u) + deg(v) ≥ n ,then  has a Hamilton circuit.
#### Dirac’s theorem
If the degree of each vertex is great than or equals n/2 in
the connected simple graph G with n vertices where n ≥ 3,
then G has a Hamilton circuit.
### Planar Graphs
In a planar representation of
- e: number of edges
- v: number of vertices
- r: number of regions
-  $r= e – v + 2$
#### Euler’s Formula
> G is a connected planar simple graph
- v ≥ 3, then e ≤ 3v – 6
- G has a vertex of degree not exceeding 5
- if v>=3 and no circuits of length 3,then e<=2v-4