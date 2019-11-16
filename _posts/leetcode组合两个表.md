---
title: 175.组合两个表（Combine Two Tables）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
表1: Person
```
+-------------+---------+
| 列名         | 类型     |
+-------------+---------+
| PersonId    | int     |
| FirstName   | varchar |
| LastName    | varchar |
+-------------+---------+
PersonId 是上表主键
```
表2: Address
```
+-------------+---------+
| 列名         | 类型    |
+-------------+---------+
| AddressId   | int     |
| PersonId    | int     |
| City        | varchar |
| State       | varchar |
+-------------+---------+
AddressId 是上表主键
```

编写一个 SQL 查询，满足条件：无论 person 是否有地址信息，都需要基于上述两表提供 person 的以下信息：

 
```
FirstName, LastName, City, State
```


# 题解

## 官方题解
### 1.使用 outer join
**思路：**
```
select FirstName, LastName, City, State
from Person left join Address
on Person.PersonId = Address.PersonId
;

```

```
select A.FirstName, A.LastName, B.City, B.State
from Person as A
left join (select distinct * from Address) as B
on A.PersonId=B.PersonId
```


## 其他题解
暂无

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/combine-two-tables/solution/zu-he-liang-ge-biao-by-leetcode/)***
