---
title: 412. Fizz Buzz (Fizz Buzz)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [412\. Fizz Buzz](https://leetcode-cn.com/problems/fizz-buzz/)

Difficulty: **简单**


写一个程序，输出从 1 到 _n_ 数字的字符串表示。

1\. 如果 _n _是3的倍数，输出“Fizz”；

2\. 如果 _n _是5的倍数，输出“Buzz”；

3.如果 _n _同时是3和5的倍数，输出 “FizzBuzz”。

**示例：**

```
n = 15,

返回:
[
    "1",
    "2",
    "Fizz",
    "4",
    "Buzz",
    "Fizz",
    "7",
    "8",
    "Fizz",
    "Buzz",
    "11",
    "Fizz",
    "13",
    "14",
    "FizzBuzz"
]
```


#### Solution

Language: **Java**

```java
​class Solution {
    public List<String> fizzBuzz(int n) {
        List<String> lst = new ArrayList<String>();
        for (int i = 1; i <= n; i++) {
            if (i % 15 == 0) {
                lst.add("FizzBuzz");
            } else if (i % 5 == 0) {
                lst.add("Buzz");
            } else if (i % 3 == 0) {
                lst.add("Fizz");
            } else {
                lst.add(String.valueOf(i));
            }
        }
        return lst;
    }
}
```

---
***参考：
[leetcode](https://leetcode-cn.com/problems/fizz-buzz/submissions/)***
