---
title: 504. 七进制数 (Base 7)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [504\. 七进制数](https://leetcode-cn.com/problems/base-7/)

Difficulty: **简单**


给定一个整数，将其转化为7进制，并以字符串形式输出。

**示例 1:**

```
输入: 100
输出: "202"
```

**示例 2:**

```
输入: -7
输出: "-10"
```

**注意:** 输入范围是 [-1e7, 1e7] 。


#### Solution

Language: **Java**

```java
​class Solution {
    public String convertToBase7(int num) {
        return Integer.toString(num, 7);
    }
}
```

```java
class Solution {
    public String convertToBase7(int num) {
        StringBuilder sb = new StringBuilder();
        int cal = Math.abs(num);
        do {
            sb.insert(0, cal % 7);
            cal /= 7;
        } while (cal != 0);
        if(num < 0) {
            sb.insert(0, "-");
        }
        return sb.toString();
    }
}
```

---
***参考:
[leetcode](https://leetcode-cn.com/problems/base-7/)***
