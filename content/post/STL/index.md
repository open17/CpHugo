---
slug: stl
title:  C++ STL
date: 2023-05-21 00:00:00+0000
categories:
    - Learn
---
## vector
```
size()
empy()
clear()
front()  back() //取值
push_back()   pop_back()
begin() end()   //迭代器
[index]
重载比较符号,字典序
```
## string
```
size()
empty()
clear()
substr(i,len) //开始下标,长度
```
## queue
```
size()
empty()
push()
front()
back()
pop()
```
## deque
```
size()
empty()
clear()
front()/back()
push_back()/pop_back()
push_front()/pop_front()
begin()/end()
[index]
```
## priority_queue
```
priority_queue<type> ,默认是大根堆(在queue库)
size()
empty()
push() 插入一个元素
top() 返回堆顶元素
pop() 弹出堆顶元素
小根堆：priority_queue<int, vector<int>, greater<int>>;
```
## stack
```
size()
empty()
push() 向栈顶插入一个元素
top() 返回栈顶元素
pop() 弹出栈顶元素
```
## pair
```
first
second
比较,first为第一关键,second为第二关键词,字典序
```
## set, map, multiset, multimap
```
size()
empty()
clear()
begin()/end()
```
### set/multiset
```
insert() 插入一个数
find() 查找一个数
count() 返回某一个数的个数
erase()
(1) 输入是一个数x，删除所有x O(k + logn)
(2) 输入一个迭代器，删除这个迭代器
lower_bound()/upper_bound()
lower_bound(x) 返回大于等于x的最小的数的迭代器
upper_bound(x) 返回大于x的最小的数的迭代器
```
### map/multimap
```
insert() 插入的数是一个pair
erase() 输入的参数是pair或者迭代器
find()
[] 注意multimap不支持此操作。 时间复杂度是 O(logn)
lower_bound()/upper_bound()
```
## unorderedXXXX
```
不支持 lower_bound()/upper_bound()， 迭代器的++，--
```
## bitset, 圧位
```
bitset<10000> s;
~, &, |, ^
>>, <<
==, !=
[]
count() 返回有多少个1
any() 判断是否至少有一个1
none() 判断是否全为0
set() 把所有位置成1
set(k, v) 将第k位变成v
reset() 把所有位变成0
flip() 等价于~
flip(k) 把第k位取反
```