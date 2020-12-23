---
title: leetcode 62. 不同路径
comments: true
categories: leetcode
tags: []
date: 2020-12-23
---

## 题目
一个机器人位于一个 m x n 网格的左上角 （起始点在下图中标记为 “Start” ）。

机器人每次只能向下或者向右移动一步。机器人试图达到网格的右下角（在下图中标记为 “Finish” ）。

问总共有多少条不同的路径？


[原题链接](http://leetcode-cn.com)
## 题解
动态规划的思想。每个格子到第一个格子的路径总数等于它上方的格子跟它左边的格子的和。因为只会用到左边的一个格子所以可以用一个一维数组替代二维的dp矩阵。

## 代码
```cpp 
class Solution {
public:
    int uniquePaths(int m, int n) {
        if(m==1 || n == 1){
            return 1;
        }
        vector<int> dp(n, 1);
        for(int i = 1; i < m; ++i){
            for(int j = 1; j < n; ++j){
                dp[j] += dp[j-1];
            }
        }
        return dp[n-1];
    }
};
```