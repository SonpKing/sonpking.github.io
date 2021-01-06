---
title: newcoder sql1. 查找最晚入职员工的所有信息
comments: true
categories: newcoder
tags: [sql]
date: 2021-01-06
---

## 题目
查找最晚入职员工的所有信息，为了减轻入门难度，目前所有的数据里员工入职的日期都不是同一天(sqlite里面的注释为--,mysql为comment)
CREATE TABLE `employees` (
`emp_no` int(11) NOT NULL,  -- '员工编号'
`birth_date` date NOT NULL,
`first_name` varchar(14) NOT NULL,
`last_name` varchar(16) NOT NULL,
`gender` char(1) NOT NULL,
`hire_date` date NOT NULL,
PRIMARY KEY (`emp_no`));

## 题解
最大值和排序两种方法

## 代码
```sql
select *
from employees
where hire_date = (
    select max(hire_date)
    from employees
);
```

```sql
select *
from employees
order by hire_date desc
limit 0,1;
```