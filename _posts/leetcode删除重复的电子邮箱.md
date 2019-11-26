---
title: 196.删除重复的电子邮箱（Delete Duplicate Emails）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [196\. 删除重复的电子邮箱](https://leetcode-cn.com/problems/delete-duplicate-emails/)

Difficulty: **简单**


编写一个 SQL 查询，来删除 `Person` 表中所有重复的电子邮箱，重复的邮箱里只保留 **Id **_最小 _的那个。

```
+----+------------------+
| Id | Email            |
+----+------------------+
| 1  | john@example.com |
| 2  | bob@example.com  |
| 3  | john@example.com |
+----+------------------+
Id 是这个表的主键。
```

例如，在运行你的查询语句之后，上面的 `Person` 表应返回以下几行:

```
+----+------------------+
| Id | Email            |
+----+------------------+
| 1  | john@example.com |
| 2  | bob@example.com  |
+----+------------------+
```


#### Solution

Language: **MySQL**

```mysql
​# Write your MySQL query statement below
delete  from Person  where id not in (select id from (select min(id) id from person group by Email)as temp )

```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/delete-duplicate-emails/)***
