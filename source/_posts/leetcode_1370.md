---
title: leetcode 1370. 上升下降字符串
comments: true
categories: leetcode
tags: [哈希表]
---

## 题目
给你一个字符串 s ，请你根据下面的算法重新构造字符串：

从 s 中选出 最小 的字符，将它 接在 结果字符串的后面。
从 s 剩余字符中选出 最小 的字符，且该字符比上一个添加的字符大，将它 接在 结果字符串后面。
重复步骤 2 ，直到你没法从 s 中选择字符。
从 s 中选出 最大 的字符，将它 接在 结果字符串的后面。
从 s 剩余字符中选出 最大 的字符，且该字符比上一个添加的字符小，将它 接在 结果字符串后面。
重复步骤 5 ，直到你没法从 s 中选择字符。
重复步骤 1 到 6 ，直到 s 中所有字符都已经被选过。
在任何一步中，如果最小或者最大字符不止一个 ，你可以选择其中任意一个，并将其添加到结果字符串。

请你返回将 s 中字符重新排序后的 结果字符串 。

示例 1：
```
输入：s = "aaaabbbbcccc"
输出："abccbaabccba"
解释：第一轮的步骤 1，2，3 后，结果字符串为 result = "abc"
第一轮的步骤 4，5，6 后，结果字符串为 result = "abccba"
第一轮结束，现在 s = "aabbcc" ，我们再次回到步骤 1
第二轮的步骤 1，2，3 后，结果字符串为 result = "abccbaabc"
第二轮的步骤 4，5，6 后，结果字符串为 result = "abccbaabccba"
```
示例 2：
```
输入：s = "rat"
输出："art"
解释：单词 "rat" 在上述算法重排序以后变成 "art"
```
## 题解
根据题意，每次在结果字符串后面追加一个先递增再递减的字符串。因为所有的字符都是小写字母，所以可以先统计26个字母的个数，然后按照从前到后和从后往前的顺序遍历，并重复直到剩余的字符串为空。假如某个字母的个数为0，那么跳过，否则将该字母加入到结果中并将该字母的个数减一。
## 代码
```cpp 
class Solution {
public:
    string sortString(string s) {
        int cnt[26] = {0};
        for(char c: s){
            ++cnt[c - 'a'];
        }
        int n = s.size();
        string res = "";
        while(res.size() < n){
            for(int i = 0; i < 26; ++i){
                if(cnt[i] > 0){
                    res.push_back('a' + i);
                    --cnt[i];
                }
            }
            for(int i = 25; i >= 0; --i){
                if(cnt[i] > 0){
                    res.push_back('a' + i);
                    --cnt[i];
                }
            }
        }
        return res;
    }
};
```