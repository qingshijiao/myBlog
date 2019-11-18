---
title: 180.连续出现的数字（Consecutive Numbers）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [179\. 最大数](https://leetcode-cn.com/problems/consecutive-numbers/)

Difficulty: **中等**


编写一个 SQL 查询，查找所有至少连续出现三次的数字。

```
+----+-----+
| Id | Num |
+----+-----+
| 1  |  1  |
| 2  |  1  |
| 3  |  1  |
| 4  |  2  |
| 5  |  1  |
| 6  |  2  |
| 7  |  2  |
+----+-----+
```

例如，给定上面的 `Logs` 表， `1` 是唯一连续出现至少三次的数字。

```
+-----------------+
| ConsecutiveNums |
+-----------------+
| 1               |
+-----------------+
```


#### Solution1

Language: **MySQL**

```mysql
​# Write your MySQL query statement below
SELECT DISTINCT
    l1.Num AS ConsecutiveNums
FROM
    Logs l1,
    Logs l2,
    Logs l3
WHERE
    l1.Id = l2.Id - 1
    AND l2.Id = l3.Id - 1
    AND l1.Num = l2.Num
    AND l2.Num = l3.Num
```

#### Solution2

Language: **MySQL**
思路用2个变量统计。pre变量统计上一次Num，cnt统计连续次数

```mysql
# Write your MySQL query statement below
​SELECT DISTINCT a.Num ConsecutiveNums FROM (
SELECT t.Num ,
       @cnt:=IF(@pre=t.Num, @cnt+1, 1) cnt,
       @pre:=t.Num pre
  FROM Logs t, (SELECT @pre:=null, @cnt:=0) b) a
  WHERE a.cnt >= 3

```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/consecutive-numbers/solution/lian-xu-chu-xian-de-shu-zi-by-leetcode/)
[hy3300](https://leetcode-cn.com/problems/consecutive-numbers/solution/bu-shi-yong-idqing-kuang-xia-tong-ji-by-hy3300/)***
