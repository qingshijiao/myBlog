---
title: 359.日志速率限制器

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### 题目
Design a logger system that receive stream of messages along with its timestamps, each message should be printed if and only if it is not printed in the last 10 seconds.

Given a message and a timestamp (in seconds granularity), return true if the message should be printed in the given timestamp, otherwise returns false.

It is possible that several messages arrive roughly at the same time.

Example:
```
Logger logger = new Logger();

// logging string "foo" at timestamp 1
logger.shouldPrintMessage(1, "foo"); returns true;

// logging string "bar" at timestamp 2
logger.shouldPrintMessage(2,"bar"); returns true;

// logging string "foo" at timestamp 3
logger.shouldPrintMessage(3,"foo"); returns false;

// logging string "bar" at timestamp 8
logger.shouldPrintMessage(8,"bar"); returns false;

// logging string "foo" at timestamp 10
logger.shouldPrintMessage(10,"foo"); returns false;

// logging string "foo" at timestamp 11
logger.shouldPrintMessage(11,"foo"); returns true;
```
设计一个接收消息流及其时间戳的日志记录系统,当且仅当在最后10秒内没有打印消息时,才应该打印每个消息.

给定消息和时间戳(以秒为粒度),如果消息应该在给定的时间戳中打印,则返回true,否则返回false.

有可能几个消息几乎同时到达.


#### Solution

Language: **Java**

```java
​class Logger{
    Map<String,Integer> shouldPrintMap;

    public Logger(){
        shouldPrintMap = new HashMap();
    }

    public boolean shouldPrintMessage(int timestamp,String message){
        boolean ans = false;
        if (!map.containsKey(message) || map.get(message) + 10 <= timestamp) {
            ans = true;
            map.put(message, timestamp);
        }
        return ans;
    }
}
```
---
***参考:
[饮酒醉回忆](https://www.jianshu.com/p/70eebfaada60)***
