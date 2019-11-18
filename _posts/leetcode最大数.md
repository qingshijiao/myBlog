---
title: 179.最大数（Largest Number）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [179\. 最大数](https://leetcode-cn.com/problems/largest-number/)

Difficulty: **中等**


给定一组非负整数，重新排列它们的顺序使之组成一个最大的整数。

**示例 1:**

```
输入: [10,2]
输出: 210
```

**示例 2:**

```
输入: [3,30,34,5,9]
输出: 9534330
```

**说明:** 输出结果可能非常大，所以你需要返回一个字符串而不是整数。


#### Solution1

Language: **Java**

```java
​class Solution {
    private class LargerNumberComparator implements Comparator<String> {
        @Override
        public int compare(String a, String b) {
            String order1 = a + b;
            String order2 = b + a;
           return order2.compareTo(order1);
        }
    }

    public String largestNumber(int[] nums) {
        // Get input integers as strings.
        String[] asStrs = new String[nums.length];
        for (int i = 0; i < nums.length; i++) {
            asStrs[i] = String.valueOf(nums[i]);
        }

        // Sort strings according to custom comparator.
        Arrays.sort(asStrs, new LargerNumberComparator());

        // If, after being sorted, the largest number is `0`, the entire number
        // is zero.
        if (asStrs[0].equals("0")) {
            return "0";
        }

        // Build largest number from sorted array.
        String largestNumberStr = new String();
        for (String numAsStr : asStrs) {
            largestNumberStr += numAsStr;
        }

        return largestNumberStr;
    }
}

```

**复杂度分析：**
- 时间复杂度：O(nlgn)
- 空间复杂度：O(n)

#### Solution2

Language: **Java**

```java
​class Solution {

    private StringBuilder res;

    public String largestNumber(int[] nums) {
        res = new StringBuilder();
        Arrays.stream(nums).boxed().map(x -> x.toString()).sorted((x, y) -> (y + x).compareTo(x + y)).forEach(x -> res.append(x));
        return res.charAt(0) == '0' ? "0" : res.toString();
    }
}

```



---
***参考：
[LeetCode](https://leetcode-cn.com/problems/largest-number/solution/zui-da-shu-by-leetcode/)
[Jasonkay](https://leetcode-cn.com/problems/largest-number/solution/java-shi-yong-lambdabiao-da-shi-he-streamsan-xing-/)***
