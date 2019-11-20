---
title: 183.从不订购的客户（Customers Who Never Order）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [183\. 从不订购的客户](https://leetcode-cn.com/problems/customers-who-never-order/)

Difficulty: **简单**


某网站包含两个表，`Customers` 表和 `Orders` 表。编写一个 SQL 查询，找出所有从不订购任何东西的客户。

`Customers` 表：

```
+----+-------+
| Id | Name  |
+----+-------+
| 1  | Joe   |
| 2  | Henry |
| 3  | Sam   |
| 4  | Max   |
+----+-------+
```

`Orders` 表：

```
+----+------------+
| Id | CustomerId |
+----+------------+
| 1  | 3          |
| 2  | 1          |
+----+------------+
```

例如给定上述表格，你的查询应返回：

```
+-----------+
| Customers |
+-----------+
| Henry     |
| Max       |
+-----------+
```


#### Solution1 - 使用子查询和 NOT IN 子句

Language: **MySQL**

```mysql
​select customers.name as 'Customers'
from customers
where customers.id not in
(
    select customerid from orders
);

```

#### Solution2 - 使用left join

Language: **MySQL**

```mysql
# Write your MySQL query statement below
select a.Name as Customers
from Customers as a
left join Orders as b
on a.Id=b.CustomerId
where b.CustomerId is null;

```


---
***参考：
[LeetCode](https://leetcode-cn.com/problems/customers-who-never-order/solution/cong-bu-ding-gou-de-ke-hu-by-leetcode/)
[houziAI](https://leetcode-cn.com/problems/customers-who-never-order/solution/tu-jie-sqlmian-shi-ti-cha-zhao-bu-zai-biao-li-de-s/)***
