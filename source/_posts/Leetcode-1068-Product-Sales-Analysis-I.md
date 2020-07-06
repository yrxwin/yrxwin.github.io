---
title: '[Leetcode 1068] Product Sales Analysis I'
categories:
  - leetcode
author: '大猩猩, 中猩猩'
date: 2020-07-02 16:11:54
tags: ['Amazon']
keywords:
description:
---
#### 原题说明
SQL Schema
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
(sale_id, year) is the primary key of this table.
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
 

Write an SQL query that reports all product names of the products in the Sales table along with their selling year and price.

For example:

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
+--------------+-------+-------+
| product_name | year  | price |
+--------------+-------+-------+
| Nokia        | 2008  | 5000  |
| Nokia        | 2009  | 5000  |
| Apple        | 2011  | 9000  |
+--------------+-------+-------+
<!--more-->

#### 解题思路
这题解法非常直接，两个表用`join`做外连接即可
#### 示例代码 (mysql)
```sql
SELECT p.product_name, s.year, s.price
FROM Sales AS s
JOIN Product AS p ON s.product_id = p.product_id
```

#### 视频讲解 
我们在**Youtube**上更新了[视频讲解](https://youtu.be/mVY4FKKTp4A)，欢迎关注！