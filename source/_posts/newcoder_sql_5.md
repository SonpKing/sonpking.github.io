---
title: NewCoder SQL5. 查找所有员工的last_name和first_name以及对应部门编号dept_no	
comments: true
categories: newcoder
tags: [sql]
date: 2021-02-24
---

## 题目

请你查找所有已经分配部门的员工的last_name和first_name以及dept_no，也包括暂时没有分配具体部门的员工

[原题链接](https://www.nowcoder.com/practice/dbfafafb2ee2482aa390645abd4463bf?tpId=82&tqId=29757&rp=1&ru=%2Fta%2Fsql&qru=%2Fta%2Fsql%2Fquestion-ranking&tab=answerKey)

## 代码
```sql
select e.last_name, e.first_name, d.dept_no
from employees as e left join dept_emp as d on e.emp_no=d.emp_no
```