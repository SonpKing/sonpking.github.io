---
title: NewCoder SQL4. 查找所有已经分配部门的员工的last_name和first_name
comments: true
categories: newcoder
tags: [sql]
date: 2021-01-28
---

## 题目

查找所有已经分配部门的员工的last_name和first_name以及dept_no(请注意输出描述里各个列的前后顺序)

[原题链接](https://www.nowcoder.com/practice/6d35b1cd593545ab985a68cd86f28671?tpId=82&&tqId=29756&rp=1&ru=/ta/sql&qru=/ta/sql/question-ranking)

## 代码
```sql
select e.last_name, e.first_name, d.dept_no
from dept_emp as d join employees as e on d.emp_no = e.emp_no
```