---
title: '[Leetcode 1050] Actors and Directors Who Cooperated At Least Three Times'
categories:
  - leetcode
author: '大猩猩, 中猩猩'
date: 2020-06-13 18:22:29
tags: ['Amazon']
keywords: 
description:
---
#### 原题说明
<div class="sql-schema-wrapper__3VBi" style="margin-bottom: 15px; color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><a class="sql-schema-link__3cEg" style="color: rgb(96, 125, 139); outline: none; cursor: pointer; transition: border-bottom-color 0.3s ease 0s; touch-action: manipulation; pointer-events: auto; padding-bottom: 1px; border-bottom: 1px solid transparent;">SQL Schema<svg viewBox="0 0 24 24" width="1em" height="1em" class="icon__3Su4"><path fill-rule="evenodd" d="M10 6L8.59 7.41 13.17 12l-4.58 4.59L10 18l6-6z"></path></svg></a></div><div style="color: rgb(38, 50, 56); font-family: -apple-system, system-ui, &quot;Segoe UI&quot;, &quot;PingFang SC&quot;, &quot;Hiragino Sans GB&quot;, &quot;Microsoft YaHei&quot;, &quot;Helvetica Neue&quot;, Helvetica, Arial, sans-serif, &quot;Apple Color Emoji&quot;, &quot;Segoe UI Emoji&quot;, &quot;Segoe UI Symbol&quot;;"><p style="font-size: inherit; margin-bottom: 1em;">Table:&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">ActorDirector</code></p><pre style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; margin-bottom: 1em; background: rgb(247, 249, 250); padding: 10px 15px; color: rgb(38, 50, 56); line-height: 1.6; border-radius: 3px; white-space: pre-wrap;">+-------------+---------+
| Column Name | Type    |
+-------------+---------+
| actor_id    | int     |
| director_id | int     |
| timestamp   | int     |
+-------------+---------+
timestamp is the primary key column for this table.
</pre><p style="font-size: inherit; margin-bottom: 1em;">&nbsp;</p><p style="font-size: inherit; margin-bottom: 1em;">Write a SQL query for a report that provides the pairs&nbsp;<code style="font-family: monospace; font-size: 13px; color: rgb(84, 110, 122); background-color: rgb(247, 249, 250); border-radius: 3px;">(actor_id, director_id)</code>&nbsp;where the actor have cooperated with the director at least 3 times.</p><p style="font-size: inherit; margin-bottom: 1em;"><span style="font-weight: bolder;">Example:</span></p><pre style="font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; margin-bottom: 1em; background: rgb(247, 249, 250); padding: 10px 15px; color: rgb(38, 50, 56); line-height: 1.6; border-radius: 3px; white-space: pre-wrap;">ActorDirector table:
+-------------+-------------+-------------+
| actor_id    | director_id | timestamp   |
+-------------+-------------+-------------+
| 1           | 1           | 0           |
| 1           | 1           | 1           |
| 1           | 1           | 2           |
| 1           | 2           | 3           |
| 1           | 2           | 4           |
| 2           | 1           | 5           |
| 2           | 1           | 6           |
+-------------+-------------+-------------+

Result table:
+-------------+-------------+
| actor_id    | director_id |
+-------------+-------------+
| 1           | 1           |
+-------------+-------------+
The only pair is (1, 1) where they cooperated exactly 3 times.</pre></div>
<!--more-->

#### 解题思路
我们需要找出一起至少合作过3次的演员和导演。
 1. 对二元组(演员,导演)分组，分别计算每组个数，选出每组个数>=3的行。
 2. 这里我们需要应用`group by`语法和`count`函数。


#### 示例代码 (mysql)
```sql
SELECT A.actor_id, A.director_id
FROM ActorDirector AS A
GROUP BY A.actor_id, A.director_id
HAVING COUNT(*) >= 3;
```


#### 归纳总结
我们在**Youtube**上更新了[视频讲解](https://youtu.be/GSc-F_jlYWk)，欢迎关注！