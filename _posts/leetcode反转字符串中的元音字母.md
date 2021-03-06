---
title: 345.反转字符串中的元音字母 (Reverse Vowels of a String)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [345\. 反转字符串中的元音字母](https://leetcode-cn.com/problems/reverse-vowels-of-a-string/)

Difficulty: **简单**


编写一个函数，以字符串作为输入，反转该字符串中的元音字母。

**示例 1:**

```
输入: "hello"
输出: "holle"
```

**示例 2:**

```
输入: "leetcode"
输出: "leotcede"
```

**说明:**
元音字母不包含字母"y"。


#### Solution

Language: **Java**

```java
​class Solution {
    public String reverseVowels(String s) {
        char[] str=s.toCharArray();
        int left=0,right=str.length-1;
        while(left<right){
            while(left<right&&str[left]!='a'&&str[left]!='e'
                 &&str[left]!='o'&&str[left]!='i'
                 &&str[left]!='u'&&str[left]!='A'
                 &&str[left]!='E'&&str[left]!='O'
                 &&str[left]!='I'&&str[left]!='U'){
                left++;
            }
            while(left<right&&str[right]!='a'&&str[right]!='e'
                 &&str[right]!='o'&&str[right]!='i'
                 &&str[right]!='u'&&str[right]!='A'
                 &&str[right]!='E'&&str[right]!='O'
                 &&str[right]!='I'&&str[right]!='U'){
                right--;
            }
            if(left<right){
                char temp=str[left];
                str[left]=str[right];
                str[right]=temp;
                left++;
                right--;
            }
        }
        return String.valueOf(str);
    }
}
```

```java
class Solution {
    public String reverseVowels(String s) {
        // 先将字符串转成字符数组（方便操作）
        // 以上是只针对 Java 语言来说的 因为 chatAt(i) 每次都要检查是否越界 有性能消耗
        char[] arr = s.toCharArray();
        int n = arr.length;
        int l = 0;
        int r = n - 1;
        while (l < r) {
            // 从左判断如果当前元素不是元音
            while (l < n && !isVowel(arr[l]) ) {
                l++;
            }
            // 从右判断如果当前元素不是元音
            while (r >= 0 && !isVowel(arr[r]) ) {
                r--;
            }
            // 如果没有元音
            if (l >= r) {
                break;
            }
            // 交换前后的元音
            swap(arr, l, r);
            // 这里要分开写，不要写进数组里面去
            l++;
            r--;
        }
        // 最后返回的时候要转换成字符串输出
        return new String(arr);
    }

    private void swap(char[] arr, int a, int b) {
        char tmp = arr[a];
        arr[a] = arr[b];
        arr[b] = tmp;
    }

    // 判断是不是元音，如果不是元音才返回 true
    private boolean isVowel(char ch) {
        // 这里要直接用 return 语句返回，不要返回 true 或者 false
         return ch == 'a' || ch == 'e' || ch == 'i' || ch == 'o' || ch == 'u'
                ||ch=='A'|| ch == 'E' || ch == 'I' || ch == 'O' || ch == 'U';
    }
}
```

---
***参考:
[leetcode](https://leetcode-cn.com/problems/reverse-vowels-of-a-string/submissions/)***
