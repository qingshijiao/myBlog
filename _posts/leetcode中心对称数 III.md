---
title: 248.中心对称数 III（Center symmetry III）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---

A strobogrammatic number is a number that looks the same when rotated 180 degrees (looked at upside down).

Write a function to count the total strobogrammatic numbers that exist in the range of low <= num <= high.

For example,
Given low = "50", high = "100", return 3. Because 69, 88, and 96 are three strobogrammatic numbers.

Note:
Because the range might be a large number, the low and high numbers are represented as string.

#### Solution - 递归

Language: **Java**

```java

public class Solution {
    public List<String> helper(int n, int max) {
        if (n == 0) return new ArrayList<String>(Arrays.asList(""));
        if (n == 1) return new ArrayList<String>(Arrays.asList("1", "8", "0"));

        List<String> list = helper(n - 2, max);
        List<String> result = new ArrayList<String>();
        for (int i = 0; i < list.size(); i++) {
            String s = list.get(i);
            if (n != max) result.add("0" + s + "0");
            result.add("1" + s + "1");
            result.add("8" + s + "8");
            result.add("6" + s + "9");
            result.add("9" + s + "6");
        }
        return result;
    }

    public int strobogrammaticInRange(String low, String high) {
        int count = 0;
        List<String> result = new ArrayList<String>();
        for (int i = low.length(); i <= high.length(); i++) {
            result.addAll(helper(i, i));
        }
        for (String str : result) {
            if (str.length() == low.length() && str.compareTo(low) < 0 || str.length() == high.length() && str.compareTo(high) > 0) continue;
            count++;
        }
        return count;
    }
}
```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/strobogrammatic-number-iii/)
[轻风舞动](https://www.cnblogs.com/lightwindy/p/8491313.html)***
