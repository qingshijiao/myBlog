---
title: 151.翻转字符串里的单词（Reverse Words in a String）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给定一个字符串，逐个翻转字符串中的每个单词。

 

示例 1：
```
输入: "the sky is blue"
输出: "blue is sky the"
```
示例 2：
```
输入: "  hello world!  "
输出: "world! hello"
解释: 输入字符串可以在前面或者后面包含多余的空格，但是反转后的字符不能包括。
```
示例 3：
```
输入: "a good   example"
输出: "example good a"
解释: 如果两个单词间有多余的空格，将反转后单词间的空格减少到只含一个。
```

**说明：**

- 无空格字符构成一个单词。
- 输入字符串可以在前面或者后面包含多余的空格，但是反转后的字符不能包括。
- 如果两个单词间有多余的空格，将反转后单词间的空格减少到只含一个。
 

**进阶：**

请选用 C 语言的用户尝试使用 O(1) 额外空间复杂度的原地解法。


# 题解

## 官方题解
暂无

## 其他题解
### 1.存入单词位一个栈
**思路：** 遍历原字符串，遇到字母就加到一个 temp 变量中，遇到空格，如果 temp 变量不为空，就把 temp 组成的单词加到一个栈中，然后清空 temp 继续遍历。

最后，将栈中的每个单词依次拿出来拼接即可。

有一个技巧可以用，就是最后一个单词后边可能没有空格，为了统一，我们可以人为的在字符串后边加入一个空格。



```
public String reverseWords(String s) {
    Stack<String> stack = new Stack<>();
    StringBuilder temp = new StringBuilder();
    s += " ";
    for (int i = 0; i < s.length(); i++) {
        if (s.charAt(i) == ' ') {
            if (temp.length() != 0) {
                stack.push(temp.toString());
                temp = new StringBuilder();
            }
        } else {
            temp.append(s.charAt(i));
        }
    }
    if (stack.isEmpty()) {
        return "";
    }
    StringBuilder res = new StringBuilder();
    res.append(stack.pop());
    while (!stack.isEmpty()) {
        res.append(" ");
        res.append(stack.pop());
    }
    return res.toString();
}



```

### 2.C语言string
**思路：** 如果用 C 语言，试着不用额外空间解决这个问题。

我们一直用的是 java，而 java 中的 String 变量是不可更改的，如果对它修改其实又会去重新创建新的内存空间。

而 C 语言不同，C 语言中的 string 本质上其实是 char 数组，所以我们可以在给定的 string 上直接进行修改而不使用额外空间。

为了曲线救国，继续用 java 实现，我们先将 String 转为 char 数组，所有的操作都在 char 数组上进行。


```
public String reverseWords(String s) {
    if (s == null) return null;

    char[] a = s.toCharArray();
    int n = a.length;

    // step 1. reverse the whole string
    reverse(a, 0, n - 1);
    // step 2. reverse each word
    reverseWords(a, n);
    // step 3. clean up spaces
    return cleanSpaces(a, n);
}

void reverseWords(char[] a, int n) {
    int i = 0, j = 0;

    while (i < n) {
        while (i < j || i < n && a[i] == ' ') i++; // skip spaces
        while (j < i || j < n && a[j] != ' ') j++; // skip non spaces
        reverse(a, i, j - 1);                      // reverse the word
    }
}

// trim leading, trailing and multiple spaces
String cleanSpaces(char[] a, int n) {
    int i = 0, j = 0;

    while (j < n) {
        while (j < n && a[j] == ' ') j++;             // skip spaces
        while (j < n && a[j] != ' ') a[i++] = a[j++]; // keep non spaces
        while (j < n && a[j] == ' ') j++;             // skip spaces
        if (j < n) a[i++] = ' ';                      // keep only one space
    }

    return new String(a).substring(0, i);
}

// reverse a[] from a[i] to a[j]
private void reverse(char[] a, int i, int j) {
    while (i < j) {
        char t = a[i];
        a[i++] = a[j];
        a[j--] = t;
    }
}


```

```
public String reverseWords(String s) {
    if (null == s || s.length() == 0)
        return "";
    final char[] c = s.toCharArray();
    final int len = c.length;
    int i = len - 1;

    while (i >= 0 && c[i] == ' ') i--;

    int left = i + 1;
    int right = i + 1;
    StringBuffer sb = new StringBuffer(i + 1);


    for (; i >= 0; i--) {
        if (c[i] == ' ') {
            if (right != left) sb.append(c, left, right - left).append(" ");
            left = i;
            right = i;
            continue;
        }
        left = i;
    }
    if (right != left)
        return sb.append(c, left, right - left).toString();
    return sb.length() > 0 ? sb.substring(0, sb.length() - 1) : "";
}

```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/reverse-words-in-a-string/submissions/)
[windliang](https://leetcode-cn.com/problems/reverse-words-in-a-string/solution/xiang-xi-tong-su-de-si-lu-fen-xi-duo-jie-fa-by-36/)
[_zhangheng](https://leetcode-cn.com/problems/reverse-words-in-a-string/solution/2-ms-ji-bai-100-java-yong-hu-by-_zhangheng/)***
