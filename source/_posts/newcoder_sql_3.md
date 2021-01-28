---
title: NewCoder SQL3. 查找各个部门当前领导当前薪水详情以及其对应部门编号dept_no
comments: true
categories: newcoder
tags: [sql]
date: 2021-01-22
---

## 题目

查找各个部门当前(dept_manager.to_date='9999-01-01')领导当前(salaries.to_date='9999-01-01')薪水详情以及其对应部门编号dept_no
(注:输出结果以salaries.emp_no升序排序，并且请注意输出结果里面dept_no列是最后一列)

[原题链接](https://www.nowcoder.com/practice/c63c5b54d86e4c6d880e4834bfd70c3b?tpId=82&&tqId=29755&rp=1&ru=/ta/sql&qru=/ta/sql/question-ranking)

## 代码
```sql
select s.emp_no, s.salary, s.from_date, s.to_date, d.dept_no
from salaries as s join dept_manager as d on s.emp_no = d.emp_no
where s.to_date = '9999-01-01' and d.to_date='9999-01-01'
```