---
title: SFSS
description: Sets, Functions, Sequences and Summations
slug: SFSS
date: 2023-05-05 00:00:00+0000
categories:
    - Math
tags:
    - Distcrete Structures
---
## Sets
- A set is a collection of objects
- Sets are used to group objects together
### Three ways to express the members in a set
    - List all the members
    - Use predicates
    - Use suspension(省略号)points(must be inferred)
### universal set
- $ℕ$ : the set of all natural numbers
- $ℤ$ : the set of integers
- $ℤ^+$ : the set of all the positive integers
- $ℚ$: the set of all rational numbers
- $ℝ$: the set of all the real numbers
- $ℂ$: the set of all complex numbers
### Venn Diagrams
- two basic shapes
    - A rectangle: indicates the universal set 
    - Circles or other shapes: indicate normal sets
### Elements and Sets
- $A∈B$ : A is in  or  is an element of B   
- $A∉B$ : A is not in  or  is not an element of B
### Subsets
- Subsets
- Proper subsets(真子集)
- Empty sets

### Cardinality
number of distinct elements in a set  
The cardinality of a set s is denoted as |s|
### Power Sets
$P(S) = {A|A ⊆ S}$  
#### Theorem of Power Sets: 
$ if |S| = n, then |P(S)| = 2^n$

### Ordered n-tuple
- The form (1, 2, … , ) or < 1, 2, … ,  >  
- (1,2) not equal to (2,1)

### Cartesian Product(笛卡尔乘积)
Cartesian product of $S_1, S_2, ⋯ ,S_n  (denoted S_1 × S_2 × ⋯ ×S_n )$    
$S_1 × S_2 × ⋯ ×S_n = \{(a1, a2, … ,an )|a_1 ∈ S_1 ∧ a_2 ∈ S_2 ∧⋯ ∧ a_n ∈ S_n\}$  
### Disjoint Sets
- If A ∩ B = ∅ then A and  B are disjoint.
- If A ∩ B ≠ ∅ then A and  B are overlapped.

## function
### conditions
> A function  from  to  is a subset of  ×  which satisfies
the following two conditions   

1.$ ∀ x(x ∈ A → ∃ y(y ∈ B ∧ (x,y) ∈f)) $  
2. $ (((x_1,y_1 ) ∈ f ∧ (x_1,y_2 ) ∈ f) → y_1 = y_2)$

### Image, Pre-image and Range(值域)
If $y = f(x)$ from set A to set B, then   
- y  is called the image of x under f
- x  is called a pre-image of y
- the set of all the images of the elements in the domain under is called the range of f, f(A) = {f(x)|x ∈ A}
### injective function（单射）
f is one-to-one
### urjective function (满射)
Onto function :$∀y ∈ B (∃x(x ∈A  ∧f (x) =y ))$
### bijective function (双射)
[One-to-One and onto function] is also called bijective function

### Floor functions
- Denoted $\lfloor x \rfloor$  
- The largest integer less than or equivalent to x
### Ceiling functions
- Denoted $\lceil x \rceil$  
- The smallest integer greater than or equivalent to x

## Sequences 数列
Sequences are ordered lists of elements
• A sequence is a function from a subset of the set of integers
({0, 1, 2, 3, … } or {1, 2, 3, … }) to a set , denoted {$a_n$}. The
integers determine the positions of the elements in the list
## Summations 求和
A summation is the value of the sum of the terms of a sequence.  
### Special Summations
#### Geometric series 等比数列和
$\sum^n_{j=0}ar^j$
#### harmonic series
$\sum^n_{j=1} \frac{1}{j}$
