---
title: 402.移掉K位数字 (Remove K Digits)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [402\. 移掉K位数字](https://leetcode-cn.com/problems/remove-k-digits/)

Difficulty: **中等**


给定一个以字符串表示的非负整数 _num_，移除这个数中的 _k_ 位数字，使得剩下的数字最小。

**注意:**

*   _num_ 的长度小于 10002 且 ≥ _k。_
*   _num_ 不会包含任何前导零。

**示例 1 :**

```
输入: num = "1432219", k = 3
输出: "1219"
解释: 移除掉三个数字 4, 3, 和 2 形成一个新的最小的数字 1219。
```

**示例 2 :**

```
输入: num = "10200", k = 1
输出: "200"
解释: 移掉首位的 1 剩下的数字为 200\. 注意输出不能有任何前导零。
```

示例 **3 :**

```
输入: num = "10", k = 2
输出: "0"
解释: 从原数字移除所有的数字，剩余为空就是0。
```


#### Solution

Language: **Java**

```java
​class Solution {
    public String removeKdigits(String num, int k) {
        StringBuilder res = new StringBuilder();
        helper(num, k, res);
        String  s = "0";
        //去首0
        for (int i = 0; i < res.length(); i++) {
            if (res.charAt(i) != '0') {
                s = res.toString().substring(i);
                break;
            }
        }
        return s;
    }

    private void helper(String num, int k, StringBuilder res) {
        //递归有两个出口
        //1.第一种情况：从n为数字中删除n个数，那就直接结束，不对res做操作。
        if (k == num.length()) return;
        //2.第二种情况：k用完了或者数字删除完了，那就将剩下的数字全都添加到res后面
        // （如果是数字用完了，那么在res后将添加一个空字符串，这是不影响结果的，所以可以合并处理）
        if (k == 0 || num.length() == 0) {
            res.append(num);
            return;
        }
        int point = -1;
        int start = 0;
        //3.找出最优的、且能通过删除数字让其成为num第一位的那个数字
        //这里拿题目中的1432219举例，第一次找到1，不删除任何数字即可让1变成第一位，剩下的数变成432219；
        //432219，找到的是第一个2，删除前面的4和3，让2变成第一位，剩下的数字变成219；
        //219，找到是第一个1，删除前面的2，让1变成第一位，剩下的是9
        //9，但k已经为0，直接返回9
        //组合历史中出现的各个第一位得到1219
        while (point == -1 || point > k){
            point = num.indexOf(Integer.toString(start));
            start++;
        }
        //修改递归参数
        res.append(--start);
        num = num.substring(point + 1);
        k -= point;
        helper(num, k, res);
    }
}
```

---
***参考:
[leetcode](https://leetcode-cn.com/problems/remove-k-digits/submissions/)***
