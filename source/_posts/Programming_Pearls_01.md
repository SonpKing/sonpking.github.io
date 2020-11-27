---
title: 编程珠玑第一章习题
comments: true
categories: 编程珠玑
tags: [C++, 题解]
date: 2020-10-31
---

### 1
> 如果不缺内存，如何使用一个具有库的语言实现一种排序算法以表示和排序集合？
```cpp 
#include<set>
int main(){
    set<int> S;
    int i;
    while(cin >> i){
        S.insert(i);
    }
    for(int j: S){
        cout<<j<<"\n";
    }
    return 0;
}
```

### 2
> 如何使用为逻辑运算（如与、或、移位）来实现位向量？
```cpp 
int a[1000]
void set(int i){
    a[i] != 1 << i;
}
void clr(int i){
    a[i] &= 1 << i;
}
int test(int i){
    return a[i] & 1 << i;
}
```

### 3
> 运行时效率是设计目标的一个重要组成部分，所得到的的程序余姚足够高效。在你自己的系统上设计实现位图排序并度量其运行时间。该时间与系统排序的运行时间以及习题1中排序的运行时间相比如何？假设n为10000000，且输入文件包含1000000个整数。



