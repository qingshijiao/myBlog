---
title: 91. 解码方法（Decode Ways）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
一条包含字母 A-Z 的消息通过以下方式进行了编码：
```
'A' -> 1
'B' -> 2
...
'Z' -> 26
```
给定一个只包含数字的非空字符串，请计算解码方法的总数。

示例 1:
```
输入: "12"
输出: 2
解释: 它可以解码为 "AB"（1 2）或者 "L"（12）。
```
示例 2:
```
输入: "226"
输出: 3
解释: 它可以解码为 "BZ" (2 26), "VF" (22 6), 或者 "BBF" (2 2 6) 。
```


# 题解

## 官方题解
暂无

## 其他题解
### 1.动态规划
**思路：**

```
class Solution {
        public int numDecodings(String s) {
            int n = s.length();
            if (n == 0) return 0;

            int[] dp = new int[n+1];
            dp[n]  = 1;
            dp[n-1] = s.charAt(n-1) != '0' ? 1 : 0;

            for (int i = n - 2; i >= 0; i--)
                if (s.charAt(i) == '0') continue;
                else dp[i] = (Integer.parseInt(s.substring(i,i+2))<=26) ? dp[i+1]+dp[i+2] : dp[i+1];

            return dp[0];
        }

}
```

### 2.动态规划2
**思路：**

```
class Solution {
    public int numDecodings(String s) {
      int len = s.length();
      int[] dp = new int[len + 1];
      dp[len] = 1; //将递归法的结束条件初始化为 1
      //最后一个数字不等于 0 就初始化为 1
      if (s.charAt(len - 1) != '0') {
          dp[len - 1] = 1;
      }
      for (int i = len - 2; i >= 0; i--) {
          //当前数字时 0 ，直接跳过，0 不代表任何字母
          if (s.charAt(i) == '0') {
              continue;
          }
          int ans1 = dp[i + 1];
          //判断两个字母组成的数字是否小于等于 26
          int ans2 = 0;
          int ten = (s.charAt(i) - '0') * 10;
          int one = s.charAt(i + 1) - '0';
          if (ten + one <= 26) {
              ans2 = dp[i + 2];
          }
          dp[i] = ans1 + ans2;

      }
      return dp[0];
  }
}
```


---
***参考：
[LeetCode](https://leetcode-cn.com/problems/decode-ways/)
[user9827R](https://leetcode-cn.com/problems/decode-ways/solution/jie-ma-fang-fa-by-user9827r/)***
