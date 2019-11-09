---
title: 161.相隔为 1 的编辑距离（One Edit Distance）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给定两个字符串 s 和 t，判断他们的编辑距离是否为 1。

注意：

满足编辑距离等于 1 有三种可能的情形：

- 往 s 中插入一个字符得到 t
- 从 s 中删除一个字符得到 t
- 在 s 中替换一个字符得到 t

示例 1：
```
输入: s = "ab", t = "acb"
输出: true
解释: 可以将 'c' 插入字符串 s 来得到 t。
```
示例 2:
```
输入: s = "cab", t = "ad"
输出: false
解释: 无法通过 1 步操作使 s 变为 t。
```
示例 3:
```
输入: s = "1203", t = "1213"
输出: true
解释: 可以将字符串 s 中的 '0' 替换为 '1' 来得到 t。
```

# 题解

## 官方题解
暂无

## 其他题解
### 1.逐一判断
**思路：**
```
public boolean isOneEditDistance(String s, String t) {
      int lenS = s.length();
      int lenT = t.length();
      int dif = Math.abs(lenS - lenT);
      if (dif > 1) {
          return false;
      }
      if (lenS > lenT) {
          return isOneEditDistance(t, s);
      }
      // 这里s指的是短的那个字符串，s比t短或者和t一样长
      for (int i = 0; i < s.length(); i++) {
          // 如果两个字符不等
          if (s.charAt(i) != t.charAt(i)) {
              if (dif == 1) {
                  return s.substring(i).equals(t.substring(i + 1));
              } else {
                  return s.substring(i + 1).equals(t.substring(i + 1));
              }
          }
      }

      return dif == 1;
  }
```

```
class Solution {
public:
    bool isOneEditDistance(string s, string t) {
        for (int i = 0; i < min(s.size(), t.size()); ++i) {
            if (s[i] != t[i]) {
                if (s.size() == t.size()) return s.substr(i + 1) == t.substr(i + 1);
                if (s.size() < t.size()) return s.substr(i) == t.substr(i + 1);
                else return s.substr(i + 1) == t.substr(i);
            }
        }
        return abs((int)s.size() - (int)t.size()) == 1;
    }
};
```

---
***参考：
[15130140362](https://blog.csdn.net/liu_12345_liu/article/details/102458599)
[grandyang](https://www.cnblogs.com/grandyang/p/5184698.html)***
