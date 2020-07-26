---
title: '[Leetcode 1069] Product Sales Analysis II'
categories:
  - leetcode
author: '大猩猩, 中猩猩'
date: 2020-07-26 19:18:31
tags: ['Amazon']
keywords: ['Amazon']
description:
---
#### 原题说明
<div class="sql-schema-wrapper__3VBi" style="margin-bottom: 15px; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><div class="content__u3I1 question-content__JfgR" style="margin: 1em 0px;"><div class="sql-schema-wrapper__3VBi" style="margin-bottom: 15px;"><a class="sql-schema-link__3cEg" style="color: rgb(96, 125, 139); outline: none; cursor: pointer; transition: border-bottom-color 0.3s ease 0s; touch-action: manipulation; pointer-events: auto; padding-bottom: 1px; border-bottom: 1px solid transparent;">SQL Schema<svg viewBox="0 0 24 24" width="1em" height="1em" class="icon__3Su4"><path fill-rule="evenodd" d="M10 6L8.59 7.41 13.17 12l-4.58 4.59L10 18l6-6z"></path></svg></a></div><div><p style="font-size: inherit; margin-bottom: 1em;">Table:&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">Sales</code></p><pre style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; margin-bottom: 1em; background: rgb(247, 249, 250); padding: 10px 15px; color: rgb(38, 50, 56); line-height: 1.6; border-radius: 3px; white-space: pre-wrap;">+-------------+-------+
| Column Name | Type  |
+-------------+-------+
| sale_id     | int   |
| product_id  | int   |
| year        | int   |
| quantity    | int   |
| price       | int   |
+-------------+-------+
sale_id is the primary key of this table.
product_id is a foreign key to <code style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; font-size: 13px; border-radius: 3px; tab-size: 4;">Product</code> table.
Note that the price is per unit.
</pre><p style="font-size: inherit; margin-bottom: 1em;">Table:&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">Product</code></p><pre style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; margin-bottom: 1em; background: rgb(247, 249, 250); padding: 10px 15px; color: rgb(38, 50, 56); line-height: 1.6; border-radius: 3px; white-space: pre-wrap;">+--------------+---------+
| Column Name  | Type    |
+--------------+---------+
| product_id   | int     |
| product_name | varchar |
+--------------+---------+
product_id is the primary key of this table.
</pre><p style="font-size: inherit; margin-bottom: 1em;">&nbsp;</p><p style="font-size: inherit; margin-bottom: 1em;">Write an SQL query that reports the total quantity sold for every product id.</p><p style="font-size: inherit; margin-bottom: 1em;">The query result format is in the following example:</p><pre style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; margin-bottom: 1em; background: rgb(247, 249, 250); padding: 10px 15px; color: rgb(38, 50, 56); line-height: 1.6; border-radius: 3px; white-space: pre-wrap;"><code style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; font-size: 13px; border-radius: 3px; tab-size: 4;">Sales</code> table:
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
+--------------+----------------+
| product_id   | total_quantity |
+--------------+----------------+
| 100          | 22             |
| 200          | 15             |
+--------------+----------------+</pre></div></div></div>
<!--more-->

#### 解题思路
不需要`Product` table, 直接 `group by product_id`即可。

#### 示例代码 (mysql)
```sql
# Write your MySQL query statement below
select product_id, sum(quantity) as total_quantity from Sales group by product_id;
```

#### 视频讲解 
我们在**Youtube**上更新了[视频讲解](https://youtu.be/vpL3f4aajqE)，欢迎关注！