---
title: 247.中心对称数 II（Center symmetry II）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---

A strobogrammatic number is a number that looks the same when rotated 180 degrees (looked at upside down).

Find all strobogrammatic numbers that are of length = n.

For example,
Given n = 2, return ["11","69","88","96"].

Hint:

Try to use recursion and notice that it should recurse with n - 2 instead of n - 1.


#### Solution - 递归

Language: **Java**

```java

public class Solution {
    public List<String> findStrobogrammatic(int n) {
        return helper(n, n);
    }

    List<String> helper(int n, int m) {
        if (n == 0) return new ArrayList<String>(Arrays.asList(""));
        if (n == 1) return new ArrayList<String>(Arrays.asList("0", "1", "8"));

        List<String> list = helper(n - 2, m);
        List<String> res = new ArrayList<String>();

        for (int i = 0; i < list.size(); i++) {
            String s = list.get(i);
            if (n != m) res.add("0" + s + "0");
            res.add("1" + s + "1");
            res.add("6" + s + "9");
            res.add("8" + s + "8");
            res.add("9" + s + "6");
        }

        return res;
    }
}

```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/strobogrammatic-number-ii/)
[轻风舞动](https://www.cnblogs.com/lightwindy/p/8491311.html)***
