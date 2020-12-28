---
title: leetcode 49. 字母异位词分组
comments: true
categories: leetcode
tags: [字典, 字符串]
date: 2020-12-14
---

## 题目
给定一个字符串数组，将字母异位词组合在一起。字母异位词指字母相同，但排列不同的字符串。

示例:
```
输入: ["eat", "tea", "tan", "ate", "nat", "bat"]
输出:

[
  ["ate","eat","tea"],
  ["nat","tan"],
  ["bat"]
]
```
[原题链接](http://leetcode-cn.com)
## 题解
本题的关键是如何让异位词变成统一的格式，然后利用字典映射统计。异位词可以通过排序的方法得到一个唯一序列，也可统计各个字符的个数然后构建一个键值。

## 代码
```cpp 
class Solution {//计数法
public:
    vector<vector<string>> groupAnagrams(vector<string>& strs) {
        unordered_map<string, vector<string>> maps;
        for(string str: strs){
            map<char, int> cnt;
            for(char c: str){
                ++cnt[c];
            }
            string ind = "";
            for(auto p: cnt){
                ind += to_string(p.first) + to_string(p.second);
            }
            maps[ind].push_back(str);
        }
        vector<vector<string>> res;
        for(auto p: maps){
            res.push_back(p.second);
        }
        return res;
    }
};
```

```cpp
class Solution {//排序法
public:
    vector<vector<string>> groupAnagrams(vector<string>& strs) {
        unordered_map<string, vector<string>> maps;
        for(string str: strs){
            string ind = str;
            sort(ind.begin(), ind.end());
            maps[ind].push_back(str);
        }
        vector<vector<string>> res;
        for(auto p: maps){
            res.push_back(p.second);
        }
        return res;
    }
};
```