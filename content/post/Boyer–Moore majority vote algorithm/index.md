---
title: 摩尔投票
slug: Boyer–Moore majority vote algorithm
tags: 
    - Boyer–Moore Majority Vote 
    - Segment Tree
date: 2023-05-28 00:00:00+0000
description: 摩尔投票是一种用来解决绝对众数问题的算法。
categories:
    - Others
---
## 什么是摩尔投票
摩尔投票是一种用来解决绝对众数[^1]问题的算法
它能使用O(1)级别的空间复杂度找出绝对众数
## 经典例题[^2]
给定一个大小为 n 的数组 nums ，返回其中的多数元素。多数元素是指在数组中出现次数 大于 ⌊ n/2 ⌋ 的元素。
```cpp
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int t=0,cnt=0;
        for(auto i:nums){
            if(i==t)cnt++;
            else if(--cnt<0){
                t=i;
                cnt=1;
            }
        }
        return t;
    }
};
```
## 区间绝对众数[^3]      
设计一个数据结构，有效地找到给定子数组的 多数元素 。         

子数组的 多数元素 是在子数组中出现 threshold 次数或次数以上的元素。            

实现 MajorityChecker 类:              

    MajorityChecker(int[] arr) 会用给定的数组 arr 对 MajorityChecker 初始化。         
    int query(int left, int right, int threshold) 返回子数组中的元素  arr[left...right] 至少出现 threshold 次数，如果不存在这样的元素则返回 -1。          
示例 1：
```
输入:
["MajorityChecker", "query", "query", "query"]
[[[1, 1, 2, 2, 1, 1]], [0, 5, 4], [0, 3, 3], [2, 3, 2]]
输出：
[null, 1, -1, 2]
解释：
MajorityChecker majorityChecker = new MajorityChecker([1,1,2,2,1,1]);
majorityChecker.query(0,5,4); // 返回 1
majorityChecker.query(0,3,3); // 返回 -1
majorityChecker.query(2,3,2); // 返回 2
```
 

提示：

    1 <= arr.length <= 2 * 104
    1 <= arr[i] <= 2 * 104
    0 <= left <= right < arr.length
    threshold <= right - left + 1
    2 * threshold > right - left + 1
    调用 query 的次数最多为 104 































## 参考
1. [通俗易懂摩尔投票法](https://leetcode.cn/problems/majority-element/solutions/2215722/tong-su-yi-dong-mo-er-tou-piao-fa-by-ni-h4m1b/)
2. [算法学习笔记(78): 摩尔投票](https://zhuanlan.zhihu.com/p/387744743)




[^1]: 在一个集合中，如果一个元素的出现次数比其他所有元素的出现次数之和还多，那么就称它为这个集合的绝对众数。等价地说，绝对众数的出现次数大于总元素数的一半。
[^2]: 题目来源:https://leetcode.cn/problems/majority-element/description/
[^3]: 题目来源LC1157. 子数组中占绝大多数的元素 