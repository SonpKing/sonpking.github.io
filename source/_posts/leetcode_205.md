---
title: leetcode 205. 同构字符串
comments: true
categories: leetcode
tags: [字典, 集合]
date: 2020-12-27
---

## 题目
给定两个字符串 s 和 t，判断它们是否是同构的。

如果 s 中的字符可以被替换得到 t ，那么这两个字符串是同构的。

所有出现的字符都必须用另一个字符替换，同时保留字符的顺序。两个字符不能映射到同一个字符上，但字符可以映射自己本身。

[原题链接](https://leetcode-cn.com/problems/isomorphic-strings/)
## 题解
本题相当于判断能不能找到两个字符串之间的一个唯一的映射。利用字典可以保存历史结果，如果遇到新的字符则假如字典；如果是旧的字符，那么到字典里查询是否正确。主要两个不同的字符不能映射到同一个字符所以，需要一个集合保存已经被映射过的字符，避免重复映射。

## 代码
```cpp 
class Solution {
public:
    bool isIsomorphic(string s, string t) {
        int n = s.size();
        if(n != t.size()){
            return false;
        }
        map<char, char> table;
        set<char> used;
        for(int i = 0; i < n; ++i){
            if(table.find(s[i])!=table.end()){
                if(table[s[i]]!=t[i]){
                    return false;
                }
            }else{
                if(used.find(t[i])==used.end()){
                    table[s[i]] = t[i];
                    used.insert(t[i]);
                }else{
                    return false;
                }
            }
        }
        return true;
    }
};
```