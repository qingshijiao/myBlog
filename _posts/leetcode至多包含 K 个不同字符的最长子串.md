---
title: 340.至多包含 K 个不同字符的最长子串

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
给定一个字符串 s ，找出 至多 包含两个不同字符的最长子串 t 。

示例 1:
```
输入: "eceba"
输出: 3
解释: t 是 "ece"，长度为3。
```
示例 2:
```
输入: "ccaabbb"
输出: 5
解释: t 是 "aabbb"，长度为5。
```

#### Solution

Language: **Java**

```java
​public static int lengthOfLongestSubstringKDistinct(String s, int k) {
        // write your code here
        int result = 0;
        int left = 0;
        //声明一个HashMap，用来存储k Distinct，还可以根据value用来判断元素是否可以删除
        HashMap<Character, Integer> map = new HashMap<>();
        for (int right = 0; right < s.length(); right++) {
            //右指针依次把字符串中的字符放到map中
            map.put(s.charAt(right),right);
            //当map元素大于k Distinct时，得到满足要求的子字符串
            while (map.size() > k) {
                // 删除最左的字符，删除成功，则退出循环
                char leftChar = s.charAt(left);
                if (map.get(leftChar) == left) {
                    map.remove(leftChar);
                }
                // 左指针右移
                left++;
            }
            //子结果即左右指针之间的长度
            int subResult = right - left + 1;
            //结果取最大
            result = Math.max(result,subResult);
        }
        return result;
    }
```

---
***参考:
[晋阳丶](https://www.jianshu.com/p/76cde56c2d85)***
