---
title: leetcode 188. 买卖股票的最佳时机 IV
comments: true
categories: leetcode
tags: [动态规划, 分类讨论]
date: 2020-12-28
---

## 题目

给定一个整数数组 prices ，它的第 i 个元素 prices[i] 是一支给定的股票在第 i 天的价格。

设计一个算法来计算你所能获取的最大利润。你最多可以完成 k 笔交易。

注意：你不能同时参与多笔交易（你必须在再次购买前出售掉之前的股票）。

[原题链接](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-iv/)
## 题解
典型的动态规划的题目。每天的状态为2种，持有股票和不持有股票。持有股票的状态可能是当日没有进行交易（交易数==前日交易数），或者当日进行了交易（交易数==前日交易数+1）；不持有股票的状态相反。用一个长度为k+1的数组记录交易数为[0, k]是进行k次交易后持有和不持有股票的最大收益。考虑到k>n相当于无限次交易，特殊考虑降低时间复杂度。

## 代码
```cpp 
class Solution {
public:
    int maxProfit(int k, vector<int>& prices) {{}
        int n = prices.size();
        if(k >= n){
            return solver1(prices);
        }else{
            return solver2(k, prices);
        }
    }

    int solver1(vector<int>& prices){
        int dp0 = 0, dp1 = -1e9;
        int n = prices.size();
        for(int i = 0; i < n; ++i){
            dp0 = max(dp0, dp1 + prices[i]);
            dp1 = max(dp1, dp0 - prices[i]);
        }
        return dp0;
    }

    int solver2(int k, vector<int>& prices){
        int n = prices.size();
        vector<int> dp0(k+1, 0);
        vector<int> dp1(k+1, -1e9);
        for(int i = 0; i < n; ++i){
            for(int j = k; j >= 1; --j){
                dp0[j] = max(dp0[j], dp1[j] + prices[i]);
                dp1[j] = max(dp1[j], dp0[j-1] - prices[i]);
            }
        }
        int res = 0;
        for(int j = 0; j <=k; ++j){
            res = max(res, dp0[j]);
        }
        return res;
    }
};
```