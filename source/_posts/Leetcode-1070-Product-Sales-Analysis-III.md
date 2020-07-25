---
title: '[Leetcode 1070] Product Sales Analysis III'
categories:
  - leetcode
author: '大猩猩, 中猩猩'
date: 2020-07-25 13:02:38
tags: ['Amazon']
keywords:
description:
---
#### 原题说明
Table: Sales

+-------------+-------+
| Column Name | Type  |
+-------------+-------+
| sale_id     | int   |
| product_id  | int   |
| year        | int   |
| quantity    | int   |
| price       | int   |
+-------------+-------+
sale_id is the primary key of this table.
product_id is a foreign key to Product table.
Note that the price is per unit.
Table: Product

+--------------+---------+
| Column Name  | Type    |
+--------------+---------+
| product_id   | int     |
| product_name | varchar |
+--------------+---------+
product_id is the primary key of this table.
 

Write an SQL query that selects the product id, year, quantity, and price for the first year of every product sold.

The query result format is in the following example:

Sales table:
+---------+------------+------+----------+-------+
| sale_id | product_id | year | quantity | price |
+---------+------------+------+----------+-------+ 
| 1       | 100        | 2008 | 10       | 5000  |
| 2       | 100        | 2009 | 12       | 5000  |
| 7       | 200        | 2011 | 15       | 9000  |
+---------+------------+------+----------+-------+

Product table:
+------------+--------------+
| product_id | product_name |
+------------+--------------+
| 100        | Nokia        |
| 200        | Apple        |
| 300        | Samsung      |
+------------+--------------+

Result table:
+------------+------------+----------+-------+
| product_id | first_year | quantity | price |
+------------+------------+----------+-------+ 
| 100        | 2008       | 10       | 5000  |
| 200        | 2011       | 15       | 9000  |
+------------+------------+----------+-------+
<!--more-->

#### 解题思路
我们需要按照年份和产品`id`分组，找出年份最小的。
要找到每个商品第一次销售的年份，我们需要应用`MIN`函数和`group by`,产生一个新的表单。 然后用`in`进行联结即可。

#### 示例代码 (mysql)
```sql
select product_id, S.year as `first_year`, quantity, price
from Sales as S
where (S.product_id, S.year) in (
    select product_id, min(year)
    from Sales
    group by product_id
)
```

#### 视频讲解 
我们在**Youtube**上更新了[视频讲解](https://youtu.be/1ErJszsDGJk)，欢迎关注！