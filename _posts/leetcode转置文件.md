---
title: 194.转置文件（Transpose File）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [194\. 转置文件](https://leetcode-cn.com/problems/transpose-file/)

Difficulty: **中等**


给定一个文件 `file.txt`，转置它的内容。

你可以假设每行列数相同，并且每个字段由 `' '` 分隔.

**示例:**

假设 `file.txt` 文件内容如下：

```
name age
alice 21
ryan 30
```

应当输出：

```
name alice ryan
age 21 30
```


#### Solution

Language: **Bash**

```bash
​# Read from the file file.txt and print its transposed content to stdout.
num=`awk 'END{print NF}' file.txt`
for i in `seq 1 $num`;do cut -d ' ' -f $i file.txt|xargs; done
```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/transpose-file/submissions/)***
