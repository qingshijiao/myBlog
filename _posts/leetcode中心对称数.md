---
title: 246.中心对称数（Center symmetry）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---

中心对称数是指一个数字在旋转了180 度之后看起来依旧相同的数字（或者上下颠倒地看）。

请写一个函数来判断该数字是否是中心对称数，其输入将会以一个字符串的形式来表达数字。

**实例1：**
```
输入:  "69"
输出: true
```

**实例2：**
```
输入:  "88"
输出: true
```

**实例3：**
```
输入:  "962"
输出: false
```


#### Solution - 双指针

Language: **Java**

```java
public class Solution {
    public boolean isStrobogrammatic(String num) {
        HashMap<Character, Character> map = new HashMap<Character, Character>();
        map.put('1','1');
        map.put('0','0');
        map.put('6','9');
        map.put('9','6');
        map.put('8','8');
        int left = 0, right = num.length() - 1;
        while(left <= right){
            if(!map.containsKey(num.charAt(right)) || num.charAt(left) != map.get(num.charAt(right))){
                return false;
            }
            left++;
            right--;
        }
        return true;
    }
}
```


---
***参考：
[LeetCode](https://leetcode-cn.com/problems/strobogrammatic-number/)
[轻风舞动](https://www.cnblogs.com/lightwindy/p/8491309.html)***
