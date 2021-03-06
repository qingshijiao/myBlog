---
title: 273.整数转换英文表示（Integer to English Words）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [273\. 整数转换英文表示](https://leetcode-cn.com/problems/integer-to-english-words/)

Difficulty: **困难**


将非负整数转换为其对应的英文表示。可以保证给定输入小于 2<sup>31</sup> - 1 。

**示例 1:**

```
输入: 123
输出: "One Hundred Twenty Three"
```

**示例 2:**

```
输入: 12345
输出: "Twelve Thousand Three Hundred Forty Five"
```

**示例 3:**

```
输入: 1234567
输出: "One Million Two Hundred Thirty Four Thousand Five Hundred Sixty Seven"
```

**示例 4:**

```
输入: 1234567891
输出: "One Billion Two Hundred Thirty Four Million Five Hundred Sixty Seven Thousand Eight Hundred Ninety One"
```


#### Solution - 分治算法

Language: **Java**

```java
​class Solution {
    public String numberToWords(int num) {
        String[] one = new String[]{"", "One", "Two", "Three", "Four", "Five", "Six", "Seven", "Eight", "Nine", "Ten", "Eleven", "Twelve", "Thirteen", "Fourteen", "Fifteen", "Sixteen", "Seventeen", "Eighteen", "Nineteen"};
        String[] two = new String[]{"Zero", "Ten", "Twenty", "Thirty", "Forty", "Fifty", "Sixty", "Seventy", "Eighty", "Ninety"};
        if(num >= 1000000000){
            if(num % 1000000000 == 0)
                return numberToWords(num / 1000000000) + " Billion";
            return numberToWords(num / 1000000000) + " Billion " + numberToWords(num % 1000000000);
        }
        if(num >= 1000000){
            if(num % 1000000 == 0)
                return numberToWords(num / 1000000) + " Million";
            return numberToWords(num / 1000000) + " Million " + numberToWords(num % 1000000);
        }
        if(num >= 1000){
            if(num % 1000 == 0)
                return numberToWords(num / 1000) + " Thousand";
            return numberToWords(num / 1000) + " Thousand " + numberToWords(num % 1000);
        }
        if(num >= 100){
            if(num % 100 == 0)
                return numberToWords(num / 100) + " Hundred";
            return numberToWords(num / 100) + " Hundred " + numberToWords(num % 100);
        }
        if(num % 10 == 0)
            return two[num/10];
        if(num > 20)
            return numberToWords(num /10 *10) + " " + numberToWords(num % 10);
        return one[num];
    }
}
```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/integer-to-english-words/submissions/)***
