---
title: leetcode 399. 除法求值
comments: true
categories: leetcode
tags: [并查集]
date: 2021-01-06
---

## 题目
给你一个变量对数组 equations 和一个实数值数组 values 作为已知条件，其中 equations[i] = [Ai, Bi] 和 values[i] 共同表示等式 Ai / Bi = values[i] 。每个 Ai 或 Bi 是一个表示单个变量的字符串。

另有一些以数组 queries 表示的问题，其中 queries[j] = [Cj, Dj] 表示第 j 个问题，请你根据已知条件找出 Cj / Dj = ? 的结果作为答案。

返回 所有问题的答案 。如果存在某个无法确定的答案，则用 -1.0 替代这个答案。

 

注意：输入总是有效的。你可以假设除法运算中不会出现除数为 0 的情况，且不存在任何矛盾的结果。

 

示例 1：
```
输入：equations = [["a","b"],["b","c"]], values = [2.0,3.0], queries = [["a","c"],["b","a"],["a","e"],["a","a"],["x","x"]]
输出：[6.00000,0.50000,-1.00000,1.00000,-1.00000]
解释：
条件：a / b = 2.0, b / c = 3.0
问题：a / c = ?, b / a = ?, a / e = ?, a / a = ?, x / x = ?
结果：[6.0, 0.5, -1.0, 1.0, -1.0 ]
```
来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/evaluate-division

## 题解
要找到两个变量的比值必须找到同一参考点，并查集中的元素的根节点可以作为这个参考点。本题需要在朴素并查集上附带权重，在寻找根节点的过程中利用链式法则改变权重，在合并时可以使用一个简单的示例辅助判断计算公式。首先为所有的变量确定一个索引，并查集的操作都是在索引上进行，避免多次字典查找。然后将每个等式进行一次合并。最后计算查询结果，如果两个变量的根节点必须是同一个节点。注意权重是根节点变量与当前变量的比值。

## 代码
```cpp 
class Solution {
public:
    vector<double> calcEquation(vector<vector<string>>& equations, vector<double>& values, vector<vector<string>>& queries) {
        unordered_map<string, int> dict;
        int n = equations.size();
        for(int i = 0, cnt = 0; i < n; ++i){
            if(dict.find(equations[i][0]) == dict.end()){
                dict[equations[i][0]] = cnt++;
            }
            if(dict.find(equations[i][1]) == dict.end()){
                dict[equations[i][1]] = cnt++;
            }
        }

        vector<int> fa(dict.size(), 0);
        vector<double> weights(dict.size(), 0);
        init(fa, weights);

        for(int i = 0; i < n; ++i){
            merge(fa, weights, dict[equations[i][0]], dict[equations[i][1]], values[i]);
        }

        n = queries.size();
        vector<double> res;
        for(int i = 0; i < n; i++){
            string x = queries[i][0], y = queries[i][1];
            if(dict.find(x) != dict.end() && dict.find(y) != dict.end() &&find(fa, weights, dict[x]) == find(fa, weights, dict[y])){
                res.push_back(weights[dict[y]] / weights[dict[x]] );
            }else{
                res.push_back(-1.0);
            }
        }
        return res;
    }

    void init(vector<int> &fa, vector<double> &weights){
        int n = fa.size();
        for(int i = 0; i < n; ++i){
            fa[i] = i;
            weights[i] = 1.0;
        }
    }

    int find(vector<int> &fa, vector<double> &weights, int x){
        if(fa[fa[x]]!=fa[x]){
            int father = find(fa, weights, fa[x]);
            weights[x] *= weights[fa[x]];
            fa[x] = father;
        }
        return fa[x];
    }

    void merge(vector<int> &fa, vector<double> &weights, int y, int x, double w){
        int fx = find(fa, weights, x);
        int fy = find(fa, weights, y);
        if(fx != fy){
            fa[fx] = fy;
            weights[fx] = w * weights[y] / weights[x];
        }
    }
};
```