---
title: 【第0002题】激活码存入数据库

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目

**第 0002 题:** 将 0001 题生成的 200 个激活码（或者优惠券）保存到 **MySQL** 关系型数据库中。

# 题解
## 1.

### 1)代码
```

#!/usr/bin/python
# -*- coding: UTF-8 -*-

import MySQLdb
import random
import string
import sys

#生成验证码
def codeMaker():
    s = "0123456789" + string.letters
    a = ""
    for i in range(4):
        for i in range(4):
            a += random.choice(s)
        if i < 4:
            a += '-'
    a = a[:-1]
    return a
#保存在文件中
file = open("test.txt",'w')
for i in range(200):
    file.write(codeMaker())
#从文件中读取并保存在str里
file = open("test.txt", "r+")
str = file.read()

# 打开数据库连接
db = MySQLdb.connect("localhost","root","","TESTDB")

# 使用cursor()方法获取操作游标
cursor = db.cursor()

# 如果数据表已经存在使用 execute() 方法删除表。
cursor.execute("DROP TABLE IF EXISTS Code")

# 创建数据表SQL语句
sql = """CREATE TABLE Code (
        Codes  CHAR(20) NOT NULL)"""

cursor.execute(sql)
# 关闭数据库连接
db.close()

# 打开数据库连接
db = MySQLdb.connect("localhost","root","","TESTDB" )

# 使用cursor()方法获取操作游标
cursor = db.cursor()
# SQL 插入语句
for n in range(200):
    sql = "INSERT INTO Code(Codes) VALUES ('%s')" % (str[19*n : 19*n+19])
    try:
        # 执行sql语句
        cursor.execute(sql)
        # 提交到数据库执行
        db.commit()
    except:
        # Rollback in case there is any error
        db.rollback()
# 关闭数据库连接
db.close()
# 关闭文件
file.close()
```

### 2)效果


### 3)说明


## 2.
### 1)代码
```
#!/usr/bin/env python
# coding: utf-8
import random
import string

# 激活码中的字符和数字
field = string.ascii_letters + string.digits


# 获得四个字母和数字的随机组合
def getRandom():
    return "".join(random.sample(field, 4))


# 生成的每个激活码中有几组
def concatenate(group):
    return "-".join([getRandom() for i in range(group)])


# 生成n组激活码
def generate(n):
    return [concatenate(4) for i in range(n)]


if __name__ == '__main__':
    print(generate(200))

```
### 2)效果
> 'Tk5X-Fi0S-BmFe-LIY6'



---
***参考：
[博客](https://blog.51cto.com/yucanghai/1715170)***
