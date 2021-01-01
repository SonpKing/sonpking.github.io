---
title: leetcode 605. 种花问题
comments: true
categories: leetcode
tags: [贪心]
date: 2021-1-1
---

## 题目


假设你有一个很长的花坛，一部分地块种植了花，另一部分却没有。可是，花卉不能种植在相邻的地块上，它们会争夺水源，两者都会死去。

给定一个花坛（表示为一个数组包含0和1，其中0表示没种植花，1表示种植了花），和一个数 n 。能否在不打破种植规则的情况下种入 n 朵花？能则返回True，不能则返回False。

示例 1:
```
输入: flowerbed = [1,0,0,0,1], n = 1
输出: True
```

示例 2:
```
输入: flowerbed = [1,0,0,0,1], n = 2
输出: False
```

注意:

> 数组内已种好的花不会违反种植规则。
> 输入的数组长度范围为 [1, 20000]。
> n 是非负整数，且不会超过输入数组的大小。

[原题链接](https://leetcode-cn.com/problems/can-place-flowers/)
## 题解
尽可能地将花种植在靠近前面的位置，可以得出结论：两个1中间间隔3个0可以插入一盆花，间隔5个0可以插入两盆花...需要注意起始和末尾为0的情况，2个0就可以插入一盆花。

## 代码
```cpp 
class Solution {
public:
    bool canPlaceFlowers(vector<int>& flowerbed, int n) {
        int m = flowerbed.size();
        int cnt = 1;
        int res = 0;
        for(int i = 0; i < m; ++i){
            if(flowerbed[i] == 0){
                ++cnt;
            }else{
                res += (cnt - 1) / 2;
                cnt = 0;
            }
        }
        res += cnt / 2;
        return res >= n;
    }
};
```