---
title:  离散数学---Tree
description: A tree is a connected undirected simple graph that contains no simple circuits.
slug: dstree
date: 2023-05-01 00:00:00+0000
categories:
    - Math
tags:
    - Distcrete Structures
    - tree
---
> A tree is a connected undirected simple graph that contains no simple circuits.
## Rooted Trees
### concept
A **rooted tree** is a tree in which *one node* has been designated the root.   
Every edge is *directed* away from the root.  
Given a vertex 𝑣 in a rooted tree 𝑇:   
- Parent: unique vertex 𝑢 such that (𝑢,𝑣) is an edge (in the direction from root to 𝑣)  
- Child: any vertex for which 𝑣 is a parent   
- Siblings : vertices with the same parent(兄弟节点)    
- Ancestors : all vertices from root to 𝑣 (except itself)  
- Descendants : vertices with 𝑣 as an ancestors  
### tips 
**A vertex of a tree is called a leaf if it has no children.**   
**Vertices that have children are called internal vertices.**     

## Game(state) Trees(决策树)
- Vertices: positions (states) in a game 
- Edges: legal moves from one position (state) to another
- Leaves: Final positions (states) of a game

## m-ary Trees(M叉树)
> A rooted tree is called 𝑚-ary if every internal vertex has no more than 𝑚 children  
- It is called full if every internal (non-leaf) vertex has exactly 𝑚 children.  
- A 2-ary tree is called a binary tree
- If vertex 𝑣 is in a tree 𝑇, the sub-tree with root 𝑣 is the tree consisting of 𝑣 and all its descendants. 

## Balanced Tree(平衡树)
### level and height
The level of a node is the length of the path from the root to the node (The level of the root is defined to be zero).    
The height of a tree is *maximum* level of node.
### balanced
A rooted 𝑚-ary tree with height ℎ is called balanced if all leaves are at levels ℎ or ℎ−1.

## Binary Search Tree (二叉搜索树)
左小右大   

## Algorithms
The presentation of an algorithm (from high level to low level):   
1. descriptive method in a natural language
2. pseudo code
3. source code

## Traversal Algorithm
### Pre-order traversal
Let 𝑇 be a rooted tree with root 𝑟. 
If 𝑇 consists only of 𝑟, then 𝑟 is the preorder traversal of 𝑇.
Otherwise, let 𝑇1 , 𝑇2 , … , 𝑇_𝑛 be the sub-trees at 𝑟 from left to right. 
The preorder traversal of 𝑇 will begin by visiting 𝑟, then 𝑇1 (in preorder), then 𝑇2 (in preorder), etc, until 𝑇𝑛 is traversed in preorder
### In-order traversal
Let 𝑇 be a rooted tree with root 𝑟 
If 𝑇 consists only of 𝑟, then 𝑟 is the in-order traversal of 𝑇.
Otherwise, let 𝑇1 , 𝑇2 , … , 𝑇_𝑛 be the sub-trees at 𝑟 from left to right. 
The in-order traversal of 𝑇 will begin by visiting 𝑇1 (in-order), then the root 𝑟, then 𝑇2 (in-order), etc, until 𝑇𝑛 is traversed in-order
### Post-order traversal
Let 𝑇 be a rooted tree with root 𝑟
If 𝑇 consists only of 𝑟, then r is the post-order traversal of 𝑇. 
Otherwise, let 𝑇1 , 𝑇2 , … , 𝑇_𝑛 be the sub-trees at 𝑟 from left to right. 
The post-order traversal of 𝑇 will begin by visiting 𝑇1 (in post-order), then 𝑇2 (in post-order), etc, then 𝑇𝑛 (in post-order) and finally the root 𝑟. 

## Expression Trees
The expression tree for an arithmetic expression consists of     
- Vertices: numbers, +, −, ∗, /, ↑(↑ represents the power function)   
- Edges: linking parts of an expression  
- Internal vertices(非叶子节点) represent operations  
- Leaves(叶子节点) represent the variables or numbers  

##  Spanning Trees(生成树)
> A spanning tree of a connected undirected graph 𝐺 is a sub-graph of 𝐺 that contains all of 𝐺’s vertices and enough of its edges to form a tree.
### How to obtain?
To obtain a spanning tree from a connected undirected graph with cycles:  
Remove edges until there are no cycles
### Depth-First Search
Depth-First Search (DFS) proceeds along a path from a vertex 𝑣 as deeply into the graph as possible before backing up (back-tracking).      
To create a depth-first search (DFS) spanning tree:     
Traverse the graph using a depth-first search and mark the edges that you follow.     
After the traversal is complete, the graph’s vertices and marked edges form the spanning tree.  
(If there are multiple choices, choose the next vertex in the alphabetical order.)
### Breadth-First Search
Breadth-First Search (BFS) visits every vertex adjacent to a vertex v that it can before visiting any other vertex.
To create a breath-first search (BFS) spanning tree
Traverse the graph using a bread-first search and mark the edges that you follow.
When the traversal is complete, the graph’s vertices and marked edges form the spanning tree.

## Minimum Spanning Trees(最小生成树)
A minimum spanning tree in a connected weighted graph is a spanning tree that has the smallest possible sum of weights of edges.   
There may be several different minimum spanning trees for a particular graph. But the minimum weight is unique.  
### Prim
1. Initially, starts from an empty (no vertices, no edges) sub minimum spanning tree 𝑇.
Randomly put a vertex 𝑣 into 𝑇.   
2. Among all the edges (𝑢,𝑠) such that 𝑢 is in 𝑇 and 𝑠 is not in 𝑇, find the one of the minimum weight.
3. And add the edge and the endpoint to 𝑇.
4. Repeat Step 3 for 𝑛−1 iterations (because a tree has 𝑛−1 edges). 

### Kruskal
- Initially, starts from a subgraph of all vertices but no edges.
- Find the edge with the smallest weight.
- If adding the smallest edge to the subgraph does not create any cycle, add it. (To maintain the tree property.)
- Otherwise,  this edge is not in the MST. So, discard the edge.
- Repeat steps 2-4 until for 𝑛−1 iterations (because a tree has 𝑛−1 edges).







