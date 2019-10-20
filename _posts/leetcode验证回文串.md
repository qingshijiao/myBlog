---
title: 125.验证回文串（Valid Palindrome）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给定一个字符串，验证它是否是回文串，只考虑字母和数字字符，可以忽略字母的大小写。

说明：本题中，我们将空字符串定义为有效的回文串。

示例 1:
```
输入: "A man, a plan, a canal: Panama"
输出: true
```
示例 2:
```
输入: "race a car"
输出: false
```

# 题解

## 官方题解
暂无

## 其他题解
### 1.双指针
**思路：**

```
public boolean isPalindrome(String s) {
    int len = s.length();
    s = s.toLowerCase(); //统一转为小写
    int i = 0, j = len - 1;
    while (i < j) {
        //跳过非法字符
        while (!isAlphanumeric(s.charAt(i))) {
            i++;
            //匹配 "   " 这样的空白字符串防止越界
            if (i == len) {
                return true;
            }
        }
        while (!isAlphanumeric(s.charAt(j))) {
            j--;
        }
        if (s.charAt(i) != s.charAt(j)) {
            return false;
        }
        i++;
        j--;
    }
    return true;
}

private boolean isAlphanumeric(char c) {
    if ('a' <= c && c <= 'z' || 'A' <= c && c <= 'Z' || '0' <= c && c <= '9') {
        return true;
    }
    return false;
}
```

### 2.映射
**思路：**

```
private static final char[] charMap = new char[256];

static {
    // 映射 '0' 到 '9'
    for (int i = 0; i < 10; i++) {
        charMap[i + '0'] = (char) (1 + i); // numeric
    }
    // 映射 'a' 到 'z' 和 映射 'A' 到 'Z'
    for (int i = 0; i < 26; i++) {
        charMap[i + 'a'] = charMap[i + 'A'] = (char) (11 + i);
    }
}

public boolean isPalindrome(String s) {
    char[] pChars = s.toCharArray();
    int start = 0, end = pChars.length - 1;
    char cS, cE;
    while (start < end) {
        // 得到映射后的数字
        cS = charMap[pChars[start]];
        cE = charMap[pChars[end]];
        if (cS != 0 && cE != 0) {
            if (cS != cE)
                return false;
            start++;
            end--;
        } else {
            if (cS == 0)
                start++;
            if (cE == 0)
                end--;
        }
    }
    return true;
}
```

### 3.字符串转字符数组
**思路：**
```
class Solution {
    public boolean isPalindrome(String s) {
        char[] array = s.toCharArray();
        int len = 0;
        int var1 = 0;
        for (int i = 0;i < array.length;i++){
            if ((array[i] >= '0' && array[i] <= '9') || (array[i] >= 'a' && array[i] <= 'z')) {
                array[len++] = array[i];
            }else if (array[i] >= 'A' && array[i] <= 'Z'){
                array[len++] = (char)(array[i] - 'A' + 'a');
            }
        }
        len--;
        while(var1 < len){
            if (array[len--] != array[var1++]){
                return false;
            }
        }
        return true;
    }
}
```



---
***参考：
[LeetCode](https://leetcode-cn.com/problems/valid-palindrome/)
[windliang](https://leetcode-cn.com/problems/valid-palindrome/solution/xiang-xi-tong-su-de-si-lu-fen-xi-duo-jie-fa-by-3-2/)***
