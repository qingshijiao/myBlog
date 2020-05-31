---
title: 451. 根据字符出现频率排序（Sort Characters By Frequency）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [451\. 根据字符出现频率排序](https://leetcode-cn.com/problems/sort-characters-by-frequency/)

Difficulty: **中等**


给定一个字符串，请将字符串里的字符按照出现的频率降序排列。

**示例 1:**

```
输入:
"tree"

输出:
"eert"

解释:
'e'出现两次，'r'和't'都只出现一次。
因此'e'必须出现在'r'和't'之前。此外，"eetr"也是一个有效的答案。
```

**示例 2:**

```
输入:
"cccaaa"

输出:
"cccaaa"

解释:
'c'和'a'都出现三次。此外，"aaaccc"也是有效的答案。
注意"cacaca"是不正确的，因为相同的字母必须放在一起。
```

**示例 3:**

```
输入:
"Aabb"

输出:
"bbAa"

解释:
此外，"bbaA"也是一个有效的答案，但"Aabb"是不正确的。
注意'A'和'a'被认为是两种不同的字符。
```


#### Solution

Language: **Java**

```java
​class Solution {
    public String frequencySort(String s) {
              if(s==null){
            return null;
        }
        char[] schar = s.toCharArray();
        int[] counter  = new int[128];
        for (char c : schar){
            counter[c]++;
        }   
        int curr =0;
        while (curr<s.length()){
            int count = 0;
            char c =0;
            for (int i=0;i<='z';i++){
                if (counter[i]>count){
                    count = counter[i];
                    c =(char) i;
                }
            }
            counter[c]=0;
            while (count-->0){
                schar[curr++] = c;
            }
        }
        return new String(schar);
    }
}
```

---
***参考：
[leetcode](https://leetcode-cn.com/problems/sort-characters-by-frequency/)***
