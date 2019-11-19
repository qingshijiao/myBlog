---
title: 182.查找重复的电子邮箱（Duplicate Emails）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [182\. 查找重复的电子邮箱](https://leetcode-cn.com/problems/duplicate-emails/)

Difficulty: **简单**


编写一个 SQL 查询，查找 `Person` 表中所有重复的电子邮箱。

**示例：**

```
+----+---------+
| Id | Email   |
+----+---------+
| 1  | a@b.com |
| 2  | c@d.com |
| 3  | a@b.com |
+----+---------+
```

根据以上输入，你的查询应返回以下结果：

```
+---------+
| Email   |
+---------+
| a@b.com |
+---------+
```

**说明：**所有电子邮箱都是小写字母。


#### Solution1 - 使用 GROUP BY 和临时表

Language: **MySQL**

```mysql
​select Email from
(
  select Email, count(Email) as num
  from Person
  group by Email
) as statistic
where num > 1
;

```

#### Solution2 - 使用 GROUP BY 和 HAVING 条件

Language: **MySQL**

```mysql
​select Email
from Person
group by Email
having count(Email) > 1;

```



---
***参考：
[LeetCode](https://leetcode-cn.com/problems/duplicate-emails/solution/cha-zhao-zhong-fu-de-dian-zi-you-xiang-by-leetcode/)***
