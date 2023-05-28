---
title: lc weekly contest 278
description: 本场竞赛由「网易游戏互娱 & 力扣」联合主办
slug: lc-weekly-contest-278 
date: 2023-05-28 00:00:00+0000
tags:
    - leetcode
    - c++
image: https://pic.lingkou.xyz/1642577172-whzTsr-1760-360%20%E5%85%AD%E6%96%B9%E4%BA%91.png
---
## 前言
题目分布:简单,中等,困难,困难  
T3卡常坐大牢  
## T1 将找到的值乘以 2
给你一个整数数组 nums ，另给你一个整数 original ，这是需要在 nums 中搜索的第一个数字。    

接下来，你需要按下述步骤操作：     

如果在 nums 中找到 original ，将 original 乘以 2 ，得到新 original（即，令 original = 2 * original）。   
否则，停止这一过程。    
只要能在数组中找到新 original ，就对新 original 继续 重复 这一过程。   
返回 original 的 最终 值。   

 

示例 1：
```
输入：nums = [5,3,6,1,12], original = 3
输出：24
```
解释：   
- 3 能在 nums 中找到。3 * 2 = 6 。
- 6 能在 nums 中找到。6 * 2 = 12 。
- 12 能在 nums 中找到。12 * 2 = 24 。
- 24 不能在 nums 中找到。因此，返回 24 。
   
示例 2：  
```
输入：nums = [2,7,9], original = 4
输出：4
```
解释：   
- 4 不能在 nums 中找到。因此，返回 4 。
 
   
提示：  
```
1 <= nums.length <= 1000
1 <= nums[i], original <= 1000
```
###  思路
由于数据范围很小,所以怎么写都行  
这里的二分还可以继续优化    
这道题还可以用哈希表达到近似O(n)    
甚至可以用位运算达到严格O(n)[^1]   
```cpp
#define debug(a,b,c) cout<<'\n'<<"debug start"<<'\n';for(int i=a;i<=b;i++){cout<<c[i]<<' ';}cout<<'\n'<<"debug over"<<'\n'<<'\n';
class Solution {
public:
    int findFinalValue(vector<int>& nums, int original) {
        sort(nums.begin(),nums.end());
        auto s=nums.begin();
        // debug(0,nums.size()-1,nums)
        while(1){
            int x=lower_bound(nums.begin(),nums.end(),original)-nums.begin();
            if (x>=nums.size()||nums[x]!=original){
                break;
            }
            original*=2;
        }
        
        return original;
    }
};
```


## T2 分组得分最高的所有下标
给你一个下标从 0 开始的二进制数组 nums ，数组长度为 n 。nums 可以按下标 i（ 0 <= i <= n ）拆分成两个数组（可能为空）：numsleft 和 numsright 。    

numsleft 包含 nums 中从下标 0 到 i - 1 的所有元素（包括 0 和 i - 1 ），而 numsright 包含 nums 中从下标 i 到 n - 1 的所有元素（包括 i 和 n - 1 ）。   
如果 i == 0 ，numsleft 为 空 ，而 numsright 将包含 nums 中的所有元素。   
如果 i == n ，numsleft 将包含 nums 中的所有元素，而 numsright 为 空 。   
下标 i 的 分组得分 为 numsleft 中 0 的个数和 numsright 中 1 的个数之 和 。   

返回 分组得分 最高 的 所有不同下标 。你可以按 任意顺序 返回答案。   

 

示例 1：
```
输入：nums = [0,0,1,0]
输出：[2,4]
```
解释：按下标分组
- 0 ：numsleft 为 [] 。numsright 为 [0,0,1,0] 。得分为 0 + 1 = 1 。
- 1 ：numsleft 为 [0] 。numsright 为 [0,1,0] 。得分为 1 + 1 = 2 。
- 2 ：numsleft 为 [0,0] 。numsright 为 [1,0] 。得分为 2 + 1 = 3 。
- 3 ：numsleft 为 [0,0,1] 。numsright 为 [0] 。得分为 2 + 0 = 2 。
- 4 ：numsleft 为 [0,0,1,0] 。numsright 为 [] 。得分为 3 + 0 = 3 。
下标 2 和 4 都可以得到最高的分组得分 3 。    
注意，答案 [4,2] 也被视为正确答案。   
   
示例 2：
```
输入：nums = [0,0,0]
输出：[3]
```
解释：按下标分组  
- 0 ：numsleft 为 [] 。numsright 为 [0,0,0] 。得分为 0 + 0 = 0 。
- 1 ：numsleft 为 [0] 。numsright 为 [0,0] 。得分为 1 + 0 = 1 。
- 2 ：numsleft 为 [0,0] 。numsright 为 [0] 。得分为 2 + 0 = 2 。
- 3 ：numsleft 为 [0,0,0] 。numsright 为 [] 。得分为 3 + 0 = 3 。
只有下标 3 可以得到最高的分组得分 3 。   
   
示例 3：   
```
输入：nums = [1,1]
输出：[0]
```
解释：按下标分组    
- 0 ：numsleft 为 [] 。numsright 为 [1,1] 。得分为 0 + 2 = 2 。
- 1 ：numsleft 为 [1] 。numsright 为 [1] 。得分为 0 + 1 = 1 。
- 2 ：numsleft 为 [1,1] 。numsright 为 [] 。得分为 0 + 0 = 0 。
只有下标 0 可以得到最高的分组得分 2 。   
 

提示： 
```
n == nums.length
1 <= n <= 105
nums[i] 为 0 或 1
```
### 思路
写的时候没仔细看题目,长度为n应该有n+1中选择情况,后来改动的时候没有保持不变量,调参调了半天     
思路: 维护前缀和即可,由sum减去得出后缀     
当然可以维护前后缀,好写一点 
这里还可以压缩成一次遍历[^2]  
```cpp
#define FOR(w, a, n) for(int w=(a);w<(n);++w)
#define debug(a,b,c) cout<<'\n'<<"debug start"<<'\n';for(int i=a;i<=b;i++){cout<<c[i]<<' ';}cout<<'\n'<<"debug over"<<'\n'<<'\n';
const int N=1e5+2;
int b[N];
class Solution {
public:
    vector<int> maxScoreIndices(vector<int>& nums) {
        int ans=0;
        FOR(i,0,nums.size()){
            //左边1的个数
            b[i+1]=b[i]+nums[i];
            ans+=nums[i];
        }
        // debug(0,nums.size(),b)
        int max_=0;
        FOR(i,0,nums.size()+1){
            max_=max(max_, i-b[i]+ans-b[i] );
        }
        vector<int> res;
        FOR(i,0,nums.size()+1){
            if(i-b[i]+ans-b[i]==max_)res.push_back(i);
        }
        return res;
    }
};
```

## T3 查找给定哈希值的子串
给定整数 p 和 m ，一个长度为 k 且下标从 0 开始的字符串 s 的哈希值按照如下函数计算：

hash(s, p, m) = (val(s[0]) * p0 + val(s[1]) * p1 + ... + val(s[k-1]) * pk-1) mod m.   
其中 val(s[i]) 表示 s[i] 在字母表中的下标，从 val('a') = 1 到 val('z') = 26 。    

给你一个字符串 s 和整数 power，modulo，k 和 hashValue 。请你返回 s 中 第一个 长度为 k 的 子串 sub ，满足 hash(sub, power, modulo) == hashValue 。    

测试数据保证一定 存在 至少一个这样的子串。   

子串 定义为一个字符串中连续非空字符组成的序列。    

 

示例 1：
```
输入：s = "leetcode", power = 7, modulo = 20, k = 2, hashValue = 0
输出："ee"
解释："ee" 的哈希值为 hash("ee", 7, 20) = (5 * 1 + 5 * 7) mod 20 = 40 mod 20 = 0 。
"ee" 是长度为 2 的第一个哈希值为 0 的子串，所以我们返回 "ee" 。
```
示例 2：
```
输入：s = "fbxzaad", power = 31, modulo = 100, k = 3, hashValue = 32
输出："fbx"
解释："fbx" 的哈希值为 hash("fbx", 31, 100) = (6 * 1 + 2 * 31 + 24 * 312) mod 100 = 23132 mod 100 = 32 。
"bxz" 的哈希值为 hash("bxz", 31, 100) = (2 * 1 + 24 * 31 + 26 * 312) mod 100 = 25732 mod 100 = 32 。
"fbx" 是长度为 3 的第一个哈希值为 32 的子串，所以我们返回 "fbx" 。
注意，"bxz" 的哈希值也为 32 ，但是它在字符串中比 "fbx" 更晚出现。
```

提示：
```
1 <= k <= s.length <= 2 * 104
1 <= power, modulo <= 109
0 <= hashValue < modulo
s 只包含小写英文字母。
测试数据保证一定 存在 满足条件的子串。
```
### 思路
先写一个暴力滑窗解法
```py
class Solution:
    def subStrHash(self, s: str, power: int, modulo: int, k: int, hashValue: int) -> str:
        def f(p,m,start,end):
            hashv=0
            for i in range(start,end+1):
                hashv+=(ord(s[i])-ord('a')+1)*(p**(i-start))
            return hashv%m
        for i in range(k-1,len(s)):
            if f(power,modulo,i-k+1,i)==hashValue:
                return s[i-k+1:i+1]
        return s
```
毫无悬念的T了    
将f尝试改成    
```py
def f(p,m,start,end):
    hashv=0
    for i in range(start,end+1):
        hashv+=(ord(s[i])-ord('a')+1)*(p**(i-start))%m
        hashv%=m
    return hashv%m
```
还是T,不过这也很正常   
如何优化?不难看出在求f函数是可以优化的,f可以由上个一个的f转移过来    
即上一个f减去第一项再除以p在加上最新一项即可   
```py
class Solution:
    def subStrHash(self, s: str, p: int, m: int, k: int, hashValue: int) -> str:
        hashv=0
        for i in range(k-1,len(s)):
            if i==k-1:
                for j in range(i-k+1,i+1):
                    hashv+=(ord(s[j])-ord('a')+1)*(p**(j-i+k-1))
            else:
                hashv-=(ord(s[i-k])-ord('a')+1)
                hashv//=p
                hashv+=(ord(s[i])-ord('a')+1)*(p**(k-1))
            if hashv%m==hashValue:
                return s[i-k+1:i+1]
            #print(hashv,i)
        return s
```
还是T?    
因为除法取余不恒等,不能分步优化     
那怎么改呢    
倒叙即可,顺便加入点优化   
```py
class Solution:
    def subStrHash(self, s: str, p: int, m: int, k: int, hashValue: int) -> str:
        hashv=0
        bas=p**(k-1)
        a=b=0
        for i in range(len(s)-1,k-2,-1):
            if i==len(s)-1:
                for j in range(i-k+1,i+1):
                    hashv+=(ord(s[j])-ord('a')+1)*(p**(j-i+k-1))%m
                    hashv%=m
            else:
                hashv-=((ord(s[i+1])-ord('a')+1)*bas)%m
                hashv%=m
                hashv*=p
                hashv%=m
                hashv+=(ord(s[i-k+1])-ord('a')+1)%m
                hashv%=m
            if hashv==hashValue:
                a=i-k+1
                b=i+1
        return s[a:b]   
```
但是,最坐牢的时刻来了,这样还是T    
快速幂的时候也引入取余,最终AC了  
### AC code 
```py
class Solution:
    def subStrHash(self, s: str, p: int, m: int, k: int, hashValue: int) -> str:
        hashv=0
        bas=pow(p,k - 1,m)
        a=b=0
        for i in range(len(s)-1,k-2,-1):
            if i==len(s)-1:
                for j in range(i-k+1,i+1):
                    hashv+=(ord(s[j])-ord('a')+1)*pow(p,j-i+k-1,m)%m
                    hashv%=m
            else:
                hashv-=((ord(s[i+1])-ord('a')+1)*bas)%m
                hashv%=m
                hashv*=p
                hashv%=m
                hashv+=(ord(s[i-k+1])-ord('a')+1)%m
                hashv%=m
            if hashv==hashValue:
                a=i-k+1
                b=i+1
        return s[a:b]
```
其实这道题主要卡时间复杂度的在幂函数这里,所以只优化幂函数,不优化后面的转移也能卡过去(即无需倒叙)[^3]

## T4 字符串分组
给你一个下标从 0 开始的字符串数组 words 。每个字符串都只包含 小写英文字母 。words 中任意一个子串中，每个字母都至多只出现一次。

如果通过以下操作之一，我们可以从 s1 的字母集合得到 s2 的字母集合，那么我们称这两个字符串为 关联的 ：   

往 s1 的字母集合中添加一个字母。   
从 s1 的字母集合中删去一个字母。   
将 s1 中的一个字母替换成另外任意一个字母,也可以替换为这个字母本身。      
数组 words 可以分为一个或者多个无交集的 组 。如果一个字符串与另一个字符串关联，那么它们应当属于同一个组。   

注意，你需要确保分好组后，一个组内的任一字符串与其他组的字符串都不关联。可以证明在这个条件下，分组方案是唯一的。    

请你返回一个长度为 2 的数组 ans ：   

ans[0] 是 words 分组后的 总组数 。   
ans[1] 是字符串数目最多的组所包含的字符串数目。   
 

示例 1：
```
输入：words = ["a","b","ab","cde"]
输出：[2,3]
```
解释：
- words[0] 可以得到 words[1] （将 'a' 替换为 'b'）和 words[2] （添加 'b'）。所以 words[0] 与 words[1] 和 words[2] 关联。
- words[1] 可以得到 words[0] （将 'b' 替换为 'a'）和 words[2] （添加 'a'）。所以 words[1] 与 words[0] 和 words[2] 关联。
- words[2] 可以得到 words[0] （删去 'b'）和 words[1] （删去 'a'）。所以 words[2] 与 words[0] 和 words[1] 关联。
- words[3] 与 words 中其他字符串都不关联。
所以，words 可以分成 2 个组 ["a","b","ab"] 和 ["cde"] 。最大的组大小为 3 。         
   
示例 2：
```
输入：words = ["a","ab","abc"]
输出：[1,3]
```
解释：        
- words[0] 与 words[1] 关联。
- words[1] 与 words[0] 和 words[2] 关联。
- words[2] 与 words[1] 关联。
由于所有字符串与其他字符串都关联，所以它们全部在同一个组内。        
所以最大的组大小为 3 。        
 

提示：
```
1 <= words.length <= 2 * 104
1 <= words[i].length <= 26
words[i] 只包含小写英文字母。
words[i] 中每个字母最多只出现一次。
```
### 思路
没时间看了  
后面再补上吧    
[见这里](https://leetcode.cn/problems/groups-of-strings/solution/)


[^1]: 可以参考[这个](https://leetcode.cn/problems/keep-multiplying-found-values-by-two/solution/ha-xi-biao-mo-ni-by-endlesscheng-ipk3/)帖子
[^2]: leetcode[官方解答](https://leetcode.cn/problems/all-divisions-with-the-highest-score-of-a-binary-array/solution/fen-zu-de-fen-zui-gao-de-suo-you-xia-bia-7pqp/)一次遍历即可
[^3]: 例如[这个](https://leetcode.cn/problems/find-substring-with-given-hash-value/solution/zheng-xiang-kao-lu-wu-da-shu-chu-li-pyth-9z4l/)预处理幂加上其它剪枝也能AC