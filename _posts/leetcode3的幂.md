---
title: 326.3的幂 (Power of Three)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [326\. 3的幂](https://leetcode-cn.com/problems/power-of-three/)

Difficulty: **简单**


给定一个整数，写一个函数来判断它是否是 3 的幂次方。

**示例 1:**

```
输入: 27
输出: true
```

**示例 2:**

```
输入: 0
输出: false
```

**示例 3:**

```
输入: 9
输出: true
```

**示例 4:**

```
输入: 45
输出: false
```

**进阶：**
你能不使用循环或者递归来完成本题吗？


#### Solution1 - 循环迭代

Language: **Java**

```java
​public class Solution {
    public boolean isPowerOfThree(int n) {
        if (n < 1) {
            return false;
        }

        while (n % 3 == 0) {
            n /= 3;
        }

        return n == 1;
    }
}
```

#### Solution2 - 基准转换

Language: **Java**

```java
​public class Solution {
    public boolean isPowerOfThree(int n) {
        return Integer.toString(n, 3).matches("^10*$");
    }
}
```

#### Solution3 - 运算法

Language: **Java**

```java
​public class Solution {
    public boolean isPowerOfThree(int n) {
        return (Math.log10(n) / Math.log10(3)) % 1 == 0;
    }
}
```

#### Solution4 - 整数限制

Language: **Java**

```java
​public class Solution {
    public boolean isPowerOfThree(int n) {
        return n > 0 && 1162261467 % n == 0;
    }
}
```


#### Solution5 - 递归

Language: **Java**

```java
class Solution {
    public boolean isPowerOfThree(int n) {
        if (n == 1) return true;
        if (n == 0) return false;
        if (n % 3 != 0) return false;
        return isPowerOfThree(n / 3);
    }
}
```

---
***参考:
[leetcode](https://leetcode-cn.com/problems/power-of-three/solution/)***
