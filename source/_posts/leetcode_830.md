---
title: leetcode 830. 较大分组的位置
comments: true
categories: leetcode
tags: [双指针, 字符串]
date: 2021-01-05
---

## 题目
在一个由小写字母构成的字符串 s 中，包含由一些连续的相同字符所构成的分组。

例如，在字符串 s = "abbxxxxzyy" 中，就含有 "a", "bb", "xxxx", "z" 和 "yy" 这样的一些分组。

分组可以用区间 [start, end] 表示，其中 start 和 end 分别表示该分组的起始和终止位置的下标。上例中的 "xxxx" 分组用区间表示为 [3,6] 。

我们称所有包含大于或等于三个连续字符的分组为 较大分组 。

找到每一个 较大分组 的区间，按起始位置下标递增顺序排序后，返回结果。

 

示例 1：
```
输入：s = "abbxxxxzzy"
输出：[[3,6]]
解释："xxxx" 是一个起始于 3 且终止于 6 的较大分组。
```
来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/positions-of-large-groups

## 题解
从前向后遍历数组，用一个指针记录分组的起始位置，如果当前字符与起始位置不同则结束该分组。注意某位分组的判断。

## 代码
```cpp 
class Solution {
public:
    vector<vector<int>> largeGroupPositions(string s) {
        int n = s.size();
        int start = 0;
        vector<vector<int>> res;
        for(int i = 1; i < n; ++i){
            if(s[i] != s[start]){
                if(i - start >= 3){
                    res.push_back(vector<int>{start, i - 1});
                }
                start = i;
            }
        }
        if(n - start >= 3){
            res.push_back(vector<int>{start, n - 1});
        }
        return res;
    }
};
```