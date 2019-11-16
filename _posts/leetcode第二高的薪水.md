---
title: 176.第二高的薪水（Second Highest Salary）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
编写一个 SQL 查询，获取 Employee 表中第二高的薪水（Salary） 。
```
+----+--------+
| Id | Salary |
+----+--------+
| 1  | 100    |
| 2  | 200    |
| 3  | 300    |
+----+--------+
```
例如上述 Employee 表，SQL查询应该返回 200 作为第二高的薪水。如果不存在第二高的薪水，那么查询应返回 null。
```
+---------------------+
| SecondHighestSalary |
+---------------------+
| 200                 |
+---------------------+
```


# 题解

## 官方题解
### 1.使用子查询和 LIMIT 子句
**思路：** 将不同的薪资按降序排序，然后使用 LIMIT 子句获得第二高的薪资。
```
SELECT
    (SELECT DISTINCT
            Salary
        FROM
            Employee
        ORDER BY Salary DESC
        LIMIT 1 OFFSET 1) AS SecondHighestSalary


```

### 2.使用 IFNULL 和 LIMIT 子句
**思路：**
```
SELECT
    IFNULL(
      (SELECT DISTINCT Salary
       FROM Employee
       ORDER BY Salary DESC
        LIMIT 1 OFFSET 1),
    NULL) AS SecondHighestSalary

```


## 其他题解
暂无

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/second-highest-salary/solution/di-er-gao-de-xin-shui-by-leetcode/)***
