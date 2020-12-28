---
title: leetcode 387. 字符串中的第一个唯一字符
comments: true
categories: leetcode
tags: [字典]
date: 2020-12-23
---

## 题目
给定一个字符串，找到它的第一个不重复的字符，并返回它的索引。如果不存在，则返回 -1。

示例：
```
s = "leetcode"
返回 0

s = "loveleetcode"
返回 2
```

[原题链接](https://leetcode-cn.com/problems/first-unique-character-in-a-string/)
## 题解
第一遍统计每个字符出现的次数，第二遍判断谁是第一个只出现一次的字符，如果没有找到则返回-1.

## 代码
```cpp 
class Solution {
public:
    int firstUniqChar(string s) {
        int cnt[26] = {0};
        for(char c: s){
            ++cnt[c - 'a'];
        }
        int n = s.size();
        for(int i = 0; i < n; i++){
            if(cnt[s[i] - 'a'] == 1){
                return i;
            }
        }
        return -1;
    }
};
```