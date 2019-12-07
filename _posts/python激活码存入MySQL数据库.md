---
title: 【第0002题】激活码存入MySQL数据库

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
#!/usr/bin/env python3
# -*- coding: utf-8 -*-


# 将0001题目中随机生成的验证码保存到MySQL数据库
import uuid
import pymysql


# 生成 num 个验证码，每个长度为length，可设置默认长度
def create_num(num, length=16):
    result = []
    while num > 0:
        uuid_id = uuid.uuid4()
        # 删去字符串中的'-',取出前length 个字符
        temp = str(uuid_id).replace('-', '')[:length]
        if temp not in result:
            result.append(temp)
            num -= 1
    return result


# 保存到MySQL数据库
def save_to_mysql(code):
    # 链接数据库
    conn = pymysql.connect(
        host='127.0.0.1',
        port=3306,
        user='root',
        passwd=None,
        db='test')

    try:
        with conn.cursor() as cursor:
            # Create a new record
            sql = "INSERT INTO `codes` (`code`) VALUES (%s)"
            cursor.execute(sql, code)

        # connection is not autocommit by default. So you must commit to save
        # your changes.
            conn.commit()

        with conn.cursor() as cursor:
            # Read a single record
            sql = "SELECT `id`, `code` FROM `codes` WHERE `code`=%s"
            cursor.execute(sql, code)
            result = cursor.fetchone()
            print(result)
    finally:
        conn.close()

for code in create_num(200):
    save_to_mysql(code)
```


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
[简书](https://www.jianshu.com/p/0970db3eb63b)***
