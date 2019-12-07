---
title: 【第0003题】激活码存入Redis数据库

date: {{date}}
categories:
- python
tags:
- python实例

---
# 题目

**第 0003 题：** 将 0001 题生成的 200 个激活码（或者优惠券）保存到 **Redis** 非关系型数据库中。

# 题解
## 1.

### 1)代码
```
#coding=utf-8
import redis
import random

r=redis.Redis(host='127.0.0.1',port=6379,db=0)

list=[]
#生成26个大写的字母
for x in range(65,91):
    a=str(chr(x))  #生成对应的ASCII码对应的字符串
    list.append(a)
#生成26个小写字母
for x in range(97,123):
    a=str(chr(x))  #生成对应的ASCII码
    list.append(a)
#生成10个数字
for x in range(10):
    list.append(str(x))
'''
def gen_code():
    a=random.sample(list,16)
    print a
'''
#生成16位激活码
def gen_code():
    s=''
    for x in range(16):
        a=random.choice(list)
        s=s+a
    return s

#生成200个激活码
for x in range(200):
    code=gen_code()
    r.set(x,code)

print 'END'
```



---
***参考：
[danation](https://blog.csdn.net/danation/article/details/76380797)***
