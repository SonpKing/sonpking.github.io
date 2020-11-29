---
title: leetcode 976. 三角形的最大周长
comments: true
categories: leetcode
tags: [快排]
date: 2020-11-29
---

## 题目
给定由一些正数（代表长度）组成的数组 A，返回由其中三个长度组成的、面积不为零的三角形的最大周长。

如果不能形成任何面积不为零的三角形，返回 0。

[原题链接](https://leetcode-cn.com/problems/largest-perimeter-triangle/)
## 题解
根据三角形的定义，任意两边之和大于第三边，两边之差小于第三边。利用三重循环，遍历每条边判断能否构成三角形并更新最大周长。此方法的时间复杂为O(n^3)。假如如果三角形三边是有序的，只要满足两小边只和大于第三边就行了。所以，我们可以先把所有长度由小到大排序，然后由后往前依次遍历找到第一个满足条件的三角形三边对的索引分别为ind, ind-1, ind-2。其中，ind为最大边，ind-2为最小边。
## 代码
```cpp 
class Solution {
public:
    int largestPerimeter(vector<int>& A) {
        int n = A.size();
        sort(A.begin(), A.end());
        for(int i = n - 1; i >= 2; --i){
            if(A[i] < A[i - 1] + A[i - 2]){
                return A[i] + A[i - 1] + A[i - 2];
            }
        }
        return 0;
    }
};
```