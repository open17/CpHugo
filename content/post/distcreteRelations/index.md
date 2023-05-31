---
title:  离散数学——Relations
description: A relation is a structure that is used to represent the relationships between elements.
slug: distcreteRelations
date: 2023-05-05 00:00:00+0000
categories:
    - Math
tags:
    - Distcrete Structures
---
>  A relation is a structure that is used to represent the relationships between elements
>
## Category of relations
- Binary relations
- N-ary relations
## Binary Relations
A binary relation R from the set 𝐴 to the set 𝐵 is a subset of 𝐴 × 𝐵.

R is a set of ordered pairs in the form (𝑎, 𝑏) where 𝑎 is from 𝐴 and 𝑏 is from 𝐵.

a R b denotes (𝑎, 𝑏) ∈ 𝑅, called 𝑎 is related to 𝑏 by R
## Functions and Relations
- Are all the functions relations? Yes
- Are all relations functions? No

## Relation on the Set
- A relation on the set is a relation from 𝐴 to 𝐴.

## Properties of Relations
### Reflexive
A relation 𝑅 on a set 𝐴 is called reflexive if (𝑎, 𝑎) ∈ 𝑅 for every element 𝑎 ∈ A
### Symmetric
A relation 𝑅 on a set 𝐴 is called symmetric if (𝑏, 𝑎) ∈ 𝑅 whenever (𝑎, 𝑏) ∈ R
###  Anti-symmetric
relation 𝑅 on a set 𝐴 is called anti-symmetric if whenever (𝑎, 𝑏) ∈ 𝑅 and (𝑏, 𝑎) ∈ 𝑅, then 𝑎 = 𝑏
### Transitive
A relation 𝑅 on a set 𝐴 is called transitive if whenever 
(𝑎, 𝑏) ∈ 𝑅 and (𝑏, 𝑐) ∈ 𝑅, then (𝑎, 𝑐) ∈ 𝑅

## Combining Relations 
The composite of 𝑅 and 𝑆 (𝑆 ◦ 𝑅): consisting of all ordered pairs (𝑎, 𝑐) where 𝑎 ∈ 𝐴, and 𝑐 ∈ 𝐶 if there exists 𝑏 such that (𝑎, 𝑏) ∈ 𝑅 and (𝑏, 𝑐) ∈ 𝑆.
>E.g.,  
▪ 𝐴 = {1}, 𝐵 = {0, 1}, 𝐶 = {2, 3}   
▪ 𝑅 = {(1, 0), (1, 1)} (a relation from 𝐴 to 𝐵)  
▪ 𝑆 = {(0, 2), (1, 3)} (a relation from 𝐵 to 𝐶)  
▪ 𝑆 ◦ 𝑅 = {(1, 2), (1, 3)}  
>
## Powers of a Relation
Let 𝑅 be a relation on the set 𝐴. The powers 𝑅𝑛
for integer 𝑛
with 𝑛 > 0 are defined recursively by 
$R^1 = R$  
$R^{n}=R^{n-1}◦R$   
>Theorem: The relation 𝑅 on a set 𝐴 is transitive if and only if 𝑅^𝑛 ⊆ 𝑅 for 𝑛 = 1, 2, 3, ⋯

## 𝑛-ary Relations
- Let 𝐴1, 𝐴2, … , 𝐴𝑛 be sets.
- An 𝑛-ary relation on these sets is a subset of 𝐴1 × 𝐴2 × ⋯ × 𝐴𝑛
- Domain: 𝐴1 × 𝐴2 × ⋯ × 𝐴𝑛
- Degree: n

## Relations and Database
- Currently, the most commonly used databases are relational databases.
- Each database consists of multiple relations.
- Each relation is presented as a table.

## Operations on n-ary Relations
### Selection operator 𝜎:
- 𝑛-ary relation 𝑅
- condition 𝑐
- Selection operator 𝜎𝑐: maps 𝑅 to an 𝑛-ary relations 𝑇, where all the tuples in 𝑇 satisfy the condition 𝑐.  
i.e. 𝜎_{𝑚𝑎𝑗𝑜𝑟}="𝐶𝑜𝑚𝑝𝑢𝑡𝑒𝑟 𝑆𝑐𝑖𝑒𝑛𝑐𝑒" 𝐺𝑟𝑎𝑑𝑒𝑅𝑒𝑝𝑜𝑟𝑡 = {(𝐽𝑜ℎ𝑛,001,𝐶𝑜𝑚𝑝𝑢𝑡𝑒𝑟 𝑆𝑐𝑖𝑒𝑛𝑐𝑒, 3.5)}

### Projection operator 𝜋:
- the input relation is on 𝑛 tuples (𝑎1, 𝑎2, ⋯ , 𝑎𝑛) ,
- the output relation is on 𝑚 tuples (𝑎𝑖_1,𝑎𝑖_2, ⋯ , 𝑎𝑖_𝑚), 𝑚 < 𝑛.
- Projection operator 𝜋𝑖1,𝑖2,⋯,𝑖𝑚: removes the tuples not in the 𝑚-tuple (𝑎𝑖1𝑎𝑖2, ⋯ , 𝑎𝑖𝑚) list
i.e. 𝜋_{𝑛𝑎𝑚𝑒,𝐺𝑃𝐴} (𝐺𝑟𝑎𝑑𝑒𝑅𝑒𝑝𝑜𝑟𝑡) = {(𝐽𝑜ℎ𝑛, 3.5 ),( 𝑇𝑜𝑛𝑦, 3.2 ),( 𝐽𝑜𝑛𝑎𝑠, 3.3)}

## Equivalence Relations
- A relation on a set 𝐴 is called an equivalence relation if it is reflexive, symmetric, and transitive.
Let 𝑅 be an equivalence relation on 𝐴.
### Equivalent class
Equivalent class -> Equivalent relations
###  Partition
- All the equivalent classes obtained from 𝐴 through an equivalent class are either same or disjoint. 
- These disjoint classes are subsets of 𝐴.
- The union of these subsets is 𝐴.
- These subsets are called a partition of A
In general, (𝐴1, 𝐴2, ⋯ , 𝐴𝑛) is a partition of 𝐴 if:
1. 𝐴𝑖 ≠ ∅ for all 1 ≤ 𝑖 ≤ 𝑛
2. 𝐴𝑖 ∩ 𝐴𝑗 = ∅ for all 1 ≤ 𝑖,𝑗 ≤ 𝑛
3. 𝐴1 ∪ 𝐴2 ∪ ⋯ ∪ 𝐴𝑛 = A
### Theorem: Let 𝑅 be an equivalence relation on a nonempty set 𝐴. 
The following statements are equivalent:
- a R b
- [𝑎] = [𝑏]
- 𝑎 ∩ [𝑏] ≠ ∅


