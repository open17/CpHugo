---
title: lc-biweekly-contest-105
description: 本场竞赛由「 Airwallex 空中云汇 & 力扣」联合主办 
slug: lc-biweekly-contest-105
date: 2023-05-27 00:00:00+0000
tags:
    - leetcode
    - c++
image: https://pic.lingkou.xyz/1683871861-YilDpq-1760-360%20%E5%AE%BD%E5%BE%B7%E6%8A%95%E8%B5%84.png
---
## 前言
待更新
## T1 购买两块巧克力   

给你一个整数数组 prices ，它表示一个商店里若干巧克力的价格。同时给你一个整数 money ，表示你一开始拥有的钱数。   

你必须购买 恰好 两块巧克力，而且剩余的钱数必须是 非负数 。同时你想最小化购买两块巧克力的总花费。   

请你返回在购买两块巧克力后，最多能剩下多少钱。如果购买任意两块巧克力都超过了你拥有的钱，请你返回 money 。注意剩余钱数必须是非负数。   

 

示例 1：  
```
输入：prices = [1,2,2], money = 3
输出：0
解释：分别购买价格为 1 和 2 的巧克力。你剩下 3 - 3 = 0 块钱。所以我们返回 0 。
```
示例 2：  
```
输入：prices = [3,2,3], money = 3
输出：3
解释：购买任意 2 块巧克力都会超过你拥有的钱数，所以我们返回 3 。
```

提示：  
```
2 <= prices.length <= 50
1 <= prices[i] <= 100
1 <= money <= 100
```
### 思路
模拟
```py
class Solution:
    def buyChoco(self, prices: List[int], money: int) -> int:
        prices.sort()
        x=money-prices[0]+prices[1]
        return x if x>=0 else money
```
## T2 字符串中的额外字符   
给你一个下标从 0 开始的字符串 s 和一个单词字典 dictionary 。你需要将 s 分割成若干个 互不重叠 的子字符串，每个子字符串都在 dictionary 中出现过。s 中可能会有一些 额外的字符 不在任何子字符串中。   

请你采取最优策略分割 s ，使剩下的字符 最少 。   

 

示例 1：
```
输入：s = "leetscode", dictionary = ["leet","code","leetcode"]
输出：1
解释：将 s 分成两个子字符串：下标从 0 到 3 的 "leet" 和下标从 5 到 8 的 "code" 。只有 1 个字符没有使用（下标为 4），所以我们返回 1 。
```
示例 2：
```
输入：s = "sayhelloworld", dictionary = ["hello","world"]
输出：3
解释：将 s 分成两个子字符串：下标从 3 到 7 的 "hello" 和下标从 8 到 12 的 "world" 。下标为 0 ，1 和 2 的字符没有使用，所以我们返回 3 。
```

提示：
```
1 <= s.length <= 50
1 <= dictionary.length <= 50
1 <= dictionary[i].length <= 50
dictionary[i] 和 s 只包含小写英文字母。
dictionary 中的单词互不相同
```
### 思路
一开始没看数据大小(真的要改),死磕kmp,然后想的是贪心处理重叠选择(很明显,至少我想了好久没找出来)    
后来回过头来看数据范围这么小,直接记忆化搜索AC(其实还wa了一发,用回溯偷懒没过)
```py
class Solution:
    def minExtraChar(self, s: str, dictionary: List[str]) -> int:
        ss=set(dictionary)
        ans=[0]
        @cache
        def dfs(i):
            if i>=len(s):
                return 0
            res=0
            for k in range(len(s)-i):
                if s[i:k+i+1] in ss:
                    res=max(dfs(k+i+1)+k+1,res)
                else:
                    res=max(res,dfs(k+i+1))
            return res
        return len(s)-dfs(0)
```
## T3 一个小组的最大实力值    
给你一个下标从 0 开始的整数数组 nums ，它表示一个班级中所有学生在一次考试中的成绩。老师想选出一部分同学组成一个 非空 小组，且这个小组的 实力值 最大，如果这个小组里的学生下标为 i0, i1, i2, ... , ik ，那么这个小组的实力值定义为 nums[i0] * nums[i1] * nums[i2] * ... * nums[ik​] 。   

请你返回老师创建的小组能得到的最大实力值为多少。   

 

示例 1：  

输入：nums = [3,-1,-5,2,5,-9]  
输出：1350  
解释：一种构成最大实力值小组的方案是选择下标为 [0,2,3,4,5] 的学生。实力值为 3 * (-5) * 2 * 5 * (-9) = 1350 ，这是可以得到的最大实力值。  
示例 2：  

输入：nums = [-4,-5,-4]  
输出：20  
解释：选择下标为 [0, 1] 的学生。得到的实力值为 20 。我们没法得到更大的实力值  
### 反思
很简单的一道题    
这里竟然wa了三发,第一发wa在少打了一个*号,第二三发wa在没注意大小写isZero和iszero 
明明本题唯一要思考的分类讨论都仔细思考了防止wa(虽然分类不够精简),却在打字上过于急躁wa   
导致排名狂掉    
以后无论代码有多简单一定要记得先测试一下能不能跑  
```py
class Solution:
    def maxStrength(self, nums: List[int]) -> int:
        ans=1
        flag=0
        p=[]
        res=1
        isZero=False
        for i in nums:
            if i>0:
                ans*=i
                flag=1
            elif i<0:
                p.append(i)
            else:
                isZero=True
        p.sort()
        size=(len(p)//2)*2
        for i in range(size):
            res*=p[i]
        if flag:
            return res*ans
        elif size>=2:
            return res
        elif isZero:
            return 0
        return p[0]
```
## T4 最大公约数遍历 
给你一个下标从 0 开始的整数数组 nums ，你可以在一些下标之间遍历。对于两个下标 i 和 j（i != j），当且仅当 gcd(nums[i], nums[j]) > 1 时，我们可以在两个下标之间通行，其中 gcd 是两个数的 最大公约数 。   

你需要判断 nums 数组中 任意 两个满足 i < j 的下标 i 和 j ，是否存在若干次通行可以从 i 遍历到 j 。   

如果任意满足条件的下标对都可以遍历，那么返回 true ，否则返回 false 。   

 

示例 1：
```
输入：nums = [2,3,6]
输出：true
解释：这个例子中，总共有 3 个下标对：(0, 1) ，(0, 2) 和 (1, 2) 。
从下标 0 到下标 1 ，我们可以遍历 0 -> 2 -> 1 ，我们可以从下标 0 到 2 是因为 gcd(nums[0], nums[2]) = gcd(2, 6) = 2 > 1 ，从下标 2 到 1 是因为 gcd(nums[2], nums[1]) = gcd(6, 3) = 3 > 1 。
从下标 0 到下标 2 ，我们可以直接遍历，因为 gcd(nums[0], nums[2]) = gcd(2, 6) = 2 > 1 。同理，我们也可以从下标 1 到 2 因为 gcd(nums[1], nums[2]) = gcd(3, 6) = 3 > 1 。
```
示例 2：
```
输入：nums = [3,9,5]
输出：false
解释：我们没法从下标 0 到 2 ，所以返回 false 。
```
示例 3：
```
输入：nums = [4,3,12,8]
输出：true
解释：总共有 6 个下标对：(0, 1) ，(0, 2) ，(0, 3) ，(1, 2) ，(1, 3) 和 (2, 3) 。所有下标对之间都存在可行的遍历，所以返回 true 。
 ```

提示：
```
1 <= nums.length <= 105
1 <= nums[i] <= 105
```
### 思路
见评论区吧