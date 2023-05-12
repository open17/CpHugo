---
title: 离散数学————Counting
description: It is the study of arrangements of objects,also called combinatorics
slug: Counting
date: 2023-05-08 00:00:00+0000
categories:
    - Math
tags:
    - Distcrete Structures
---
## Basic Counting Principles
### The product rule
乘法原理
#### Exercise
•Prove Theorem: $ if |S| = n, then |P(S)| = 2^n$
### The sum rule
加法原理
### The Inclusion-Exclusion Principle
容斥原理
### The Pigeonhole Principle
抽屉原理
#### Theorem 1: 
If k is a positive integer and k + 1 or more objects are placed into k boxes, then there is at least one box containing two or more of the objects.
#### Theorem 2: 
If n objects are placed into k boxes, then there is at least one box containing at least n/k objects.

## Permutation
排列（考虑顺序）
$P(n, r) = n!/(n  −  r)!$
## Combination
组合（不考虑顺序）
$C(n, r), or (^n_r)$
### 隔板法
How many solutions does the equation a + b + c = 11
have where a, b, and c are non-negative integers?
## Binomial Coefficients
二项式定理：     
![公式](https://bkimg.cdn.bcebos.com/formula/90e7897708ac2d3e2619efc1fd9071ff.svg)
## Recurrence Relations
### Linear Homogeneous recurrence relation 
Theorem 1:     
Let $c_1$ and $c_2$ be real numbers. Suppose that $r^2 – c_1 – c_2 = 0$ has two distinct roots $r_1$ and $r_2$. Then the sequence $\{a_n\}$ is a solution of the recurrence relation $a_n= c_1a_{n-1} + c_2a_{n-2}$ if and only if $a_n= k_1r_1^n+k_2r_2^n$ for $n  = 0, 1, 2, …,$ where $k_1$ and $k_2$ are constants.


