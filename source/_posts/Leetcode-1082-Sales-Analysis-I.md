---
title: '[Leetcode 1082] Sales Analysis I'
categories:
  - leetcode
author: '大猩猩, 中猩猩'
date: 2020-08-12 18:00:20
tags:
keywords:
description:
---
#### 原题说明
<p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">Table:&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">Product</code></p><pre style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; margin-bottom: 1em; background: rgb(247, 249, 250); padding: 10px 15px; color: rgb(38, 50, 56); line-height: 1.6; border-radius: 3px; white-space: pre-wrap;">+--------------+---------+
| Column Name  | Type    |
+--------------+---------+
| product_id   | int     |
| product_name | varchar |
| unit_price   | int     |
+--------------+---------+
product_id is the primary key of this table.
</pre><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">Table:&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">Sales</code></p><pre style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; margin-bottom: 1em; background: rgb(247, 249, 250); padding: 10px 15px; color: rgb(38, 50, 56); line-height: 1.6; border-radius: 3px; white-space: pre-wrap;">+-------------+---------+
| Column Name | Type    |
+-------------+---------+
| seller_id   | int     |
| product_id  | int     |
| buyer_id    | int     |
| sale_date   | date    |
| quantity    | int     |
| price       | int     |
+------ ------+---------+
This table has no primary key, it can have repeated rows.
product_id is a foreign key to Product table.
</pre><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">&nbsp;</p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">Write an SQL query that reports the best&nbsp;<span style="font-weight: bolder;">seller</span>&nbsp;by total sales price, If there is a tie, report them all.</p><p style="font-size: 14px; margin-bottom: 1em; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;">The query result format is in the following example:</p><pre style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; margin-bottom: 1em; background: rgb(247, 249, 250); padding: 10px 15px; color: rgb(38, 50, 56); line-height: 1.6; border-radius: 3px; white-space: pre-wrap;">Product table:
+------------+--------------+------------+
| product_id | product_name | unit_price |
+------------+--------------+------------+
| 1          | S8           | 1000       |
| 2          | G4           | 800        |
| 3          | iPhone       | 1400       |
+------------+--------------+------------+

<code style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; font-size: 13px; border-radius: 3px; tab-size: 4;">Sales </code>table:
+-----------+------------+----------+------------+----------+-------+
| seller_id | product_id | buyer_id | sale_date  | quantity | price |
+-----------+------------+----------+------------+----------+-------+
| 1         | 1          | 1        | 2019-01-21 | 2        | 2000  |
| 1         | 2          | 2        | 2019-02-17 | 1        | 800   |
| 2         | 2          | 3        | 2019-06-02 | 1        | 800   |
| 3         | 3          | 4        | 2019-05-13 | 2        | 2800  |
+-----------+------------+----------+------------+----------+-------+

Result table:
+-------------+
| seller_id   |
+-------------+
| 1           |
| 3           |
+-------------+
Both sellers with id 1 and 3 sold products with the most total price of 2800.</pre>
<!--more-->

#### 解题思路
题目要求找出最好的`seller`，如果有一样，那就把他们都找出来。我们需要注意两点：
1. `Sales`表中的`price`是`unit_price`与`quantity`的乘积，所以直接将表中对应`seller`每行的`price`加和即为销售额。所以，这就需要对`seller_id`使用`GROUP BY`后再`SUM(price)`。
2. 得到每个`seller`的总销售额以后，按总销售额降序排列，用`LIMIT 1`取第一个。但这带来的问题是，如果有平手，则无法全部取出。解决方法是，先使用一个子查询得到最好的`seller`的销售额，然后再查询销售额等于这个的`seller`即可。

#### 示例代码 (mysql)
```sql
SELECT seller_id
FROM Sales
GROUP BY seller_id
HAVING SUM(price) = (SELECT SUM(price) as pr
					 FROM Sales
                     GROUP BY seller_id
                     ORDER BY pr DESC
                     LIMIT 1 )
```


#### 视频讲解 
我们在**Youtube**上更新了[视频讲解](https://youtu.be/nA0FdLBZwEs)，欢迎关注！