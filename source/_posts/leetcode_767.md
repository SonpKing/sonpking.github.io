---
title: leetcode 767. 重构字符串
comments: true
categories: leetcode
tags: [优先队列, 哈希表, 贪心]
date: 2020-11-30
---

## 题目
给定一个字符串S，检查是否能重新排布其中的字母，使得两相邻的字符不同。

若可行，输出任意可行的结果。若不可行，返回空字符串。

[原题链接](https://leetcode-cn.com/problems/reorganize-string/)
## 题解
先统计每个字符出现的个数，然后维护一个优先队列按照字符的个数排序。每取一个字符则将它的个数减去一，如果个数为零则从优先队列中益处。当前被取用的字符在下次不能使用，保存在`last`变量里。最后判断得到的字符的长度是否和原字符长度相等，如果不想等则说明还有连续重复的字符未取尽。
## 代码
```cpp 
class Solution {
public:
    string reorganizeString(string S) {
        map<char, int> cnt;
        for(char c: S){
            ++cnt[c];
        }
        priority_queue<pair<int, char>> que;
        for(pair<char, int> p: cnt){
            que.push(make_pair(p.second, p.first));
        }
        pair<int, char> last = {0, 'a'};
        pair<int, char> tmp;
        string res = "";
        while(!que.empty()){
            tmp = que.top();
            que.pop();
            res.push_back(tmp.second);
            if(--last.first > 0){
                que.push(last);
            }
            last = tmp;
        }
        return res.size() == S.size()? res: "";
    }
};
```