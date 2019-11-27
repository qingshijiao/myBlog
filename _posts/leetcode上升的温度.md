---
title: 197.上升的温度（Rising Temperature）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [197\. 上升的温度](https://leetcode-cn.com/problems/rising-temperature/)

Difficulty: **简单**


给定一个 `Weather` 表，编写一个 SQL 查询，来查找与之前（昨天的）日期相比温度更高的所有日期的 Id。

```
+---------+------------------+------------------+
| Id(INT) | RecordDate(DATE) | Temperature(INT) |
+---------+------------------+------------------+
|       1 |       2015-01-01 |               10 |
|       2 |       2015-01-02 |               25 |
|       3 |       2015-01-03 |               20 |
|       4 |       2015-01-04 |               30 |
+---------+------------------+------------------+
```

例如，根据上述给定的 `Weather` 表格，返回如下 Id:

```
+----+
| Id |
+----+
|  2 |
|  4 |
+----+
```


#### Solution

Language: **MySQL**

```mysql
​# Write your MySQL query statement below
select result.id from (
    select
    id,
    if(w.Temperature>@prevTemp and datediff(w.RecordDate,@prevDate)=1,1,0) as high,
    @prevTemp:=w.Temperature,
    @prevDate:=w.RecordDate
    from
    (select * from weather order by RecordDate) as w,
    (select @prevDate:=Temperature,@prevTemp:=Temperature from Weather order by RecordDate limit 1) as initPrevTemp
) as result where result.high=1 order by id
```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/rising-temperature/submissions/)***
