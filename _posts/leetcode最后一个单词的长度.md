---
title: 58. 最后一个单词的长度（Length of Last Word）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给定一个仅包含大小写字母和空格 ' ' 的字符串，返回其最后一个单词的长度。

如果不存在最后一个单词，请返回 0 。

说明：一个单词是指由字母组成，但不包含任何空格的字符串。

示例:
```
输入: "Hello World"
输出: 5
```



# 题解

## 官方题解
暂无

## 其他题解
### 1.删除末尾空格 + 从后开始遍历
**思路：**
```
class Solution {
    public int lengthOfLastWord(String s) {
        int end = s.length() - 1;
        while(end >= 0 && s.charAt(end) == ' ') end--;
        if(end < 0) return 0;
        int start = end;
        while(start >= 0 && s.charAt(start) != ' ') start--;
        return end - start;
    }

}
```


---
***参考：
[LeetCode](https://leetcode-cn.com/problems/length-of-last-word/)
[guanpengchn](https://leetcode-cn.com/problems/length-of-last-word/solution/hua-jie-suan-fa-58-zui-hou-yi-ge-dan-ci-de-chang-d/)***
