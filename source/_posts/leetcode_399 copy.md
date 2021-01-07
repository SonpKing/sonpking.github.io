---
title: leetcode 547. 省份数量
comments: true
categories: leetcode
tags: [dfs, 并查集]
date: 2021-01-07
---

## 题目
有 n 个城市，其中一些彼此相连，另一些没有相连。如果城市 a 与城市 b 直接相连，且城市 b 与城市 c 直接相连，那么城市 a 与城市 c 间接相连。

省份 是一组直接或间接相连的城市，组内不含其他没有相连的城市。

给你一个 n x n 的矩阵 isConnected ，其中 isConnected[i][j] = 1 表示第 i 个城市和第 j 个城市直接相连，而 isConnected[i][j] = 0 表示二者不直接相连。

返回矩阵中 省份 的数量。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/number-of-provinces

## 题解
本题与寻找海中独立的岛屿相类似，从一个点出发遍历它能到达的所有的点并标记，把它们看做一个整体。遍历图中的所有点，如果该点已经被访问了则放弃，否则计数增加1。

## 代码
```cpp 
class Solution {
public:
    int findCircleNum(vector<vector<int>>& isConnected) {
        int n = isConnected.size();
        vector<bool> vis(n, false);
        int res = 0;
        for(int i = 0; i < n; ++i){
            if(!vis[i]){
                dfs(isConnected, vis, i);
                ++res;
            }
        }
        return res;
    }

    void dfs(vector<vector<int>>& isConnected, vector<bool> &vis, int i){
        for(int j = 0, n = isConnected.size(); j < n; ++j){
            if(!vis[j] && isConnected[i][j] == 1){
                vis[j] = true;
                dfs(isConnected, vis, j);
            }
        }
    }
};
```