---
title: leetcode 435. 无重叠区间
comments: true
categories: leetcode
tags: [贪心]
date: 2020-12-31
---

## 题目


给定一个区间的集合，找到需要移除区间的最小数量，使剩余区间互不重叠。

注意:

可以认为区间的终点总是大于它的起点。
区间 [1,2] 和 [2,3] 的边界相互“接触”，但没有相互重叠。
示例 1:
```
输入: [ [1,2], [2,3], [3,4], [1,3] ]

输出: 1

解释: 移除 [1,3] 后，剩下的区间没有重叠。
```
[原题链接](https://leetcode-cn.com/problems/non-overlapping-intervals/)
## 题解
每次优先选择最小末端的线段，过滤掉起始小于末端的那些线段

## 代码
```cpp 
class Solution {
public:
    static bool cmp(const vector<int>& interval1, const vector<int>& interval2){
        return  interval1[1] < interval2[1];
    }

    int eraseOverlapIntervals(vector<vector<int>>& intervals) {
        sort(intervals.begin(), intervals.end(), cmp);
        int n = intervals.size();
        int cnt = 0;
        int last_ind = -1e9;
        for(int i = 0; i < n; ++i){
            if(intervals[i][0]>=last_ind){
                ++cnt;
                last_ind = intervals[i][1];
            }
        }
        return n - cnt;
    }
};
```