---
title: 177.第N高的薪水（Nth Highest Salary）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [177\. 第N高的薪水](https://leetcode-cn.com/problems/nth-highest-salary/)

Difficulty: **中等**


编写一个 SQL 查询，获取 `Employee` 表中第 _n _高的薪水（Salary）。

```
+----+--------+
| Id | Salary |
+----+--------+
| 1  | 100    |
| 2  | 200    |
| 3  | 300    |
+----+--------+
```

例如上述 `Employee` 表，_n = 2 _时，应返回第二高的薪水 `200`。如果不存在第 _n _高的薪水，那么查询应返回 `null`。

```
+------------------------+
| getNthHighestSalary(2) |
+------------------------+
| 200                    |
+------------------------+
```


#### Solution

Language: **MySQL**

```mysql
​CREATE FUNCTION getNthHighestSalary(N INT) RETURNS INT
BEGIN
  SET n = N-1;
  RETURN (
      # Write your MySQL query statement below.

      # SELECT IFNULL((SELECT  Distinct Salary From Employee order by Salary DESC LIMIT n,1), NULL)
      SELECT  Distinct Salary From Employee order by Salary DESC LIMIT n,1
      # n后的第一条，即第n条记录

  );
END
```


---
***参考：
[LeetCode](https://leetcode-cn.com/problems/nth-highest-salary/submissions/)***
