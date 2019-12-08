---
title: 【第0021题】密码加密

date: {{date}}
categories:
- python
tags:
- python实例
---

# 题目

**第 0021 题：** 通常，登陆某个网站或者 APP，需要使用用户名和密码。密码是如何加密后存储起来的呢？请使用 Python 对密码加密。

- 阅读资料 [用户密码的存储与 Python 示例](http://zhuoqiang.me/password-storage-and-python-example.html)

- 阅读资料 [Hashing Strings with Python](http://www.pythoncentral.io/hashing-strings-with-python/)

- 阅读资料 [Python's safest method to store and retrieve passwords from a database](

# 题解
## 1.

### 1)代码
```python
# !/usr/bin/env python
# -*- coding: utf-8 -*-

import uuid
import hashlib


def hash_password(password):
    # uuid is used to generate a random number
    salt = uuid.uuid4().hex
    return hashlib.sha256(salt.encode() + password.encode()).hexdigest() + ':' + salt


def check_password(hashed_password, user_password):
    password, salt = hashed_password.split(':')
    return password == hashlib.sha256(salt.encode() + user_password.encode()).hexdigest()


if __name__ == '__main__':
    new_pass = input('Please enter a password: ')
    hashed_password = hash_password(new_pass)
    print('The string to store in the db is: ' + hashed_password)
    old_pass = input('Now please enter the password again to check: ')
    if check_password(hashed_password, old_pass):
        print('You entered the right password')
    else:
        print('I am sorry but the password does not match')

```

### 2) 效果

```
Please enter a password: 123456
The string to store in the db is: 0e83c9e3c5b81017d345141cd33a260fa74b75e5b33916a16a1835687f2bc500:88982063db584a2d9d98176f642a3850
Now please enter the password again to check: 12345
I am sorry but the password does not match
```

---
***参考：
[Hashing Strings with Python](https://www.pythoncentral.io/hashing-strings-with-python/)***
