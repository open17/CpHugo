---
title: lc weekly contest 348 
description: 思维场
slug: lc-weekly-contest-348 
date: 2023-06-03 00:00:00+0000
tags:
    - Leetcode
image: https://img2.baidu.com/it/u=4248933948,3175621791&fm=253&app=138&size=w931&n=0&f=JPEG&fmt=auto?sec=1686330000&t=53c71f720e5610b35567333cb516b465;
---
## 写在前面
难度: 中等简单中等困难    
前三题均为思维题   最后一题比较板   
## T1  最小化字符串长度
```
给你一个下标从 0 开始的字符串 s ，重复执行下述操作 任意 次：

在字符串中选出一个下标 i ，并使 c 为字符串下标 i 处的字符。并在 i 左侧（如果有）和 右侧（如果有）各 删除 一个距离 i 最近 的字符 c 。
请你通过执行上述操作任意次，使 s 的长度 最小化 。

返回一个表示 最小化 字符串的长度的整数。

 

示例 1：

输入：s = "aaabc"
输出：3
解释：在这个示例中，s 等于 "aaabc" 。我们可以选择位于下标 1 处的字符 'a' 开始。接着删除下标 1 左侧最近的那个 'a'（位于下标 0）以及下标 1 右侧最近的那个 'a'（位于下标 2）。执行操作后，字符串变为 "abc" 。继续对字符串执行任何操作都不会改变其长度。因此，最小化字符串的长度是 3 。
示例 2：

输入：s = "cbbd"
输出：3
解释：我们可以选择位于下标 1 处的字符 'b' 开始。下标 1 左侧不存在字符 'b' ，但右侧存在一个字符 'b'（位于下标 2），所以会删除位于下标 2 的字符 'b' 。执行操作后，字符串变为 "cbd" 。继续对字符串执行任何操作都不会改变其长度。因此，最小化字符串的长度是 3 。
示例 3：

输入：s = "dddaaa"
输出：2
解释：我们可以选择位于下标 1 处的字符 'd' 开始。接着删除下标 1 左侧最近的那个 'd'（位于下标 0）以及下标 1 右侧最近的那个 'd'（位于下标 2）。执行操作后，字符串变为 "daaa" 。继续对新字符串执行操作，可以选择位于下标 2 的字符 'a' 。接着删除下标 2 左侧最近的那个 'a'（位于下标 1）以及下标 2 右侧最近的那个 'a'（位于下标 3）。执行操作后，字符串变为 "da" 。继续对字符串执行任何操作都不会改变其长度。因此，最小化字符串的长度是 2 。
 

提示：

1 <= s.length <= 100
s 仅由小写英文字母组成
```
### 思路
手玩几个即可得出结论: 结果等于有多少个不同的字符
#### 结论的简单证明:
1. 由于题目是删除最近的c字符,因此重新排序对结果没有影响
2. 为了使证明更直观,我们重新排序,将所有相同字符的放在一起
3. 要证明` 结果等于有多少个不同的字符`等价于证明所有相同字符无论多长都能删除到只剩下一个
4. 当相同字符长度为1时,显然成立
5. 当长为2时也成立
6. 设相同字符长度为n和n-1(n-1>2)时,也能能删除到只剩下一个
7. 则当相同字符长度为n+1时,由于通过定义我们可以删除第n个字符的左右,则长度变为n-1,又因为n-1可以删除到只剩下一个,所以对于长度为n+1也成立
8. 由于4 5 6 7可知`所有相同字符无论多长都能删除到只剩下一个`成立
9. 综上,结论成立
### code
```cpp
class Solution {
public:
    int minimizedStringLength(string s) {
        set<char> ss;
        for(auto i:s){
            ss.insert(i);
        }
        return ss.size();
    }
};
```
## T2
```
给你一个下标从 0 开始、长度为 n 的整数排列 nums 。

如果排列的第一个数字等于 1 且最后一个数字等于 n ，则称其为 半有序排列 。你可以执行多次下述操作，直到将 nums 变成一个 半有序排列 ：

选择 nums 中相邻的两个元素，然后交换它们。
返回使 nums 变成 半有序排列 所需的最小操作次数。

排列 是一个长度为 n 的整数序列，其中包含从 1 到 n 的每个数字恰好一次。

 

示例 1：

输入：nums = [2,1,4,3]
输出：2
解释：可以依次执行下述操作得到半有序排列：
1 - 交换下标 0 和下标 1 对应元素。排列变为 [1,2,4,3] 。
2 - 交换下标 2 和下标 3 对应元素。排列变为 [1,2,3,4] 。
可以证明，要让 nums 成为半有序排列，不存在执行操作少于 2 次的方案。
示例 2：

输入：nums = [2,4,1,3]
输出：3
解释：
可以依次执行下述操作得到半有序排列：
1 - 交换下标 1 和下标 2 对应元素。排列变为 [2,1,4,3] 。
2 - 交换下标 0 和下标 1 对应元素。排列变为 [1,2,4,3] 。
3 - 交换下标 2 和下标 3 对应元素。排列变为 [1,2,3,4] 。
可以证明，要让 nums 成为半有序排列，不存在执行操作少于 3 次的方案。
示例 3：

输入：nums = [1,3,4,2,5]
输出：0
解释：这个排列已经是一个半有序排列，无需执行任何操作。
 

提示：

2 <= nums.length == n <= 50
1 <= nums[i] <= 50
nums 是一个 排列
```
### 思路
贪心,可以看出要次数最小,1不可能往右交换,len不可能往左
那找到各个下标即可   
然后如果len在1左边,记得答案减一/下标+1即可(或者先算len,那就反过来)
```py
class Solution:
    def semiOrderedPermutation(self, nums: List[int]) -> int:
        n=len(nums)
        if nums[0]==1 and nums[-1]==n:
            return 0
        p1=pn=-1
        for i,j in enumerate(nums):
            if j==1:
                p1=i
            elif j==n:
                pn=i
        if pn<p1:
            pn+=1
        return p1+n-pn-1
```
## T3
```
给你一个整数 n 和一个下标从 0 开始的 二维数组 queries ，其中 queries[i] = [typei, indexi, vali] 。

一开始，给你一个下标从 0 开始的 n x n 矩阵，所有元素均为 0 。每一个查询，你需要执行以下操作之一：

    如果 typei == 0 ，将第 indexi 行的元素全部修改为 vali ，覆盖任何之前的值。
    如果 typei == 1 ，将第 indexi 列的元素全部修改为 vali ，覆盖任何之前的值。

请你执行完所有查询以后，返回矩阵中所有整数的和。
```
 

示例 1：
![](https://assets.leetcode.com/uploads/2023/05/11/exm1.png)
```
输入：n = 3, queries = [[0,0,1],[1,2,2],[0,2,3],[1,0,4]]
输出：23
解释：上图展示了每个查询以后矩阵的值。所有操作执行完以后，矩阵元素之和为 23 。
```
示例 2：
![](https://assets.leetcode.com/uploads/2023/05/11/exm2.png)
```
输入：n = 3, queries = [[0,0,4],[0,1,2],[1,0,1],[0,2,3],[1,2,1]]
输出：17
解释：上图展示了每一个查询操作之后的矩阵。所有操作执行完以后，矩阵元素之和为 17 。
```
 
```
提示：

    1 <= n <= 104
    1 <= queries.length <= 5 * 104
    queries[i].length == 3
    0 <= typei <= 1
    0 <= indexi < n
    0 <= vali <= 105
```
### 思路
正难则反,思维题
```cpp
class Solution:
    def matrixSumQueries(self, n: int, queries: List[List[int]]) -> int:
        row=set()
        col=set()
        ans=0
        for i in range(len(queries)-1,-1,-1):
            t,j,v=queries[i]
            if t==1:
                if j not in col:
                    ans+=(n-len(row))*v
                    col.add(j)
            if t==0:
                if j not in row:
                    ans+=(n-len(col))*v
                    row.add(j)
        return ans
```
## T4
```
给你两个数字字符串 num1 和 num2 ，以及两个整数 max_sum 和 min_sum 。如果一个整数 x 满足以下条件，我们称它是一个好整数：

    num1 <= x <= num2
    min_sum <= digit_sum(x) <= max_sum.

请你返回好整数的数目。答案可能很大，请返回答案对 109 + 7 取余后的结果。

注意，digit_sum(x) 表示 x 各位数字之和。

 

示例 1：

输入：num1 = "1", num2 = "12", min_num = 1, max_num = 8
输出：11
解释：总共有 11 个整数的数位和在 1 到 8 之间，分别是 1,2,3,4,5,6,7,8,10,11 和 12 。所以我们返回 11 。

示例 2：

输入：num1 = "1", num2 = "5", min_num = 1, max_num = 5
输出：5
解释：数位和在 1 到 5 之间的 5 个整数分别为 1,2,3,4 和 5 。所以我们返回 5 。

 

提示：

    1 <= num1 <= num2 <= 1022
    1 <= min_sum <= max_sum <= 400
```
注: 1022=$10^{22}$
### 思路
数位DP,这里是直接改的板子,is_num其实不需要
```py
class Solution:
    def S(self,s: str,min_sum: int, max_sum: int):
        @cache  
        def f(i: int, mask: int, is_limit: bool, is_num: bool) -> int:
            if max_sum<mask:
                return 0
            if i == len(s):
                return int(mask>=min_sum) 
            res = 0
            low = 0 if is_num else 1  
            up = int(s[i]) if is_limit else 9 
            for d in range(low, up + 1): 
                    res += f(i + 1, mask+d, is_limit and d == up, True)
            return res%int(1e9+7)
        return f(0, 0, True, True)
    def count(self, num1: str, num2: str, min_sum: int, max_sum: int) -> int:
        return self.S(num2,min_sum,max_sum)-self.S(num1,min_sum,max_sum)+(min_sum <= sum(map(int, num1)) <= max_sum)
```
