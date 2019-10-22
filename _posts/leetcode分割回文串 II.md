---
title: 132.分割回文串 II（Palindrome Partitioning II）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给定一个字符串 s，将 s 分割成一些子串，使每个子串都是回文串。

返回符合要求的最少分割次数。

示例:
```
输入: "aab"
输出: 1
解释: 进行一次分割就可将 s 分割成 ["aa","b"] 这样两个回文子串。
```


# 题解

## 官方题解
暂无


## 其他题解

### 1.分治法优化
**思路：**


```
class Solution {
    public int minCut(String s) {
        boolean[][] dp = new boolean[s.length()][s.length()];
        int[] min = new int[s.length()];
        min[0] = 0;
        for (int i = 1; i < s.length(); i++) {
            int temp = Integer.MAX_VALUE;
            for (int j = 0; j <= i; j++) {
                if (s.charAt(j) == s.charAt(i) && (j + 1 > i - 1 || dp[j + 1][i - 1])) {
                    dp[j][i] = true;
                    if (j == 0) {
                        temp = 0;
                    } else {
                        temp = Math.min(temp, min[j - 1] + 1);
                    }
                }
            }
            min[i] = temp;

        }
        return min[s.length() - 1];

    }
}
```

### 2.回溯法
**思路：**


```
class Solution {
    public int minCut(String s) {
        boolean[][] dp = new boolean[s.length()][s.length()];
        int[] min = new int[s.length()];
        min[0] = 0;
        for (int i = 1; i < s.length(); i++) {
            int temp = Integer.MAX_VALUE;
            for (int j = 0; j <= i; j++) {
                if (s.charAt(j) == s.charAt(i) && (j + 1 > i - 1 || dp[j + 1][i - 1])) {
                    dp[j][i] = true;
                    if (j == 0) {
                        temp = 0;
                    } else {
                        temp = Math.min(temp, min[j - 1] + 1);
                    }
                }
            }
            min[i] = temp;

        }
        return min[s.length() - 1];

    }
}
```

### 3.中心扩展法
**思路：**


```
class Solution {
    public int minCut(String s) {
        int[] dp = new int[s.length()];
        int n = s.length();
        //假设没有任何的回文串，初始化 dp
        for (int i = 0; i < n; i++) {
            dp[i] = i;
        }

        // 考虑每个中心
        for (int i = 0; i < s.length(); i++) {
            // j 表示某一个方向扩展的个数
            int j = 0;
            // 考虑奇数的情况
            while (true) {
                if (i - j < 0 || i + j > n - 1) {
                    break;
                }
                if (s.charAt(i - j) == s.charAt(i + j)) {
                    if (i - j == 0) {
                        dp[i + j] = 0;
                    } else {
                        dp[i + j] = Math.min(dp[i + j], dp[i - j - 1] + 1);
                    }

                } else {
                    break;
                }
                j++;
            }

            // j 表示某一个方向扩展的个数
            j = 1;
            // 考虑偶数的情况
            while (true) {
                if (i - j + 1 < 0 || i + j > n - 1) {
                    break;
                }
                if (s.charAt(i - j + 1) == s.charAt(i + j)) {
                    if (i - j + 1 == 0) {
                        dp[i + j] = 0;
                    } else {
                        dp[i + j] = Math.min(dp[i + j], dp[i - j + 1 - 1] + 1);
                    }

                } else {
                    break;
                }
                j++;
            }

        }
        return dp[n - 1];
    }
}
```

```
class Solution {
    public int minCut(String s) {
        if(s == null || s.length() <= 1)
            return 0;
        int len = s.length();
        int dp[] = new int[len];
        Arrays.fill(dp, len-1);
        for(int i = 0; i < len; i++){
            // 注意偶数长度与奇数长度回文串的特点
            mincutHelper(s , i , i , dp);  // 奇数回文串以1个字符为中心
            mincutHelper(s, i , i+1 , dp); // 偶数回文串以2个字符为中心
        }
        return dp[len-1];
    }
    private void mincutHelper(String s, int i, int j, int[] dp){
        int len = s.length();
        while(i >= 0 && j < len && s.charAt(i) == s.charAt(j)){
            dp[j] = Math.min(dp[j] , (i==0?-1:dp[i-1])+1);
            i--;
            j++;
        }
    }
}
```



---
***参考：
[LeetCode](https://leetcode-cn.com/problems/palindrome-partitioning-ii/submissions/)
[windliang](https://leetcode-cn.com/problems/palindrome-partitioning-ii/solution/xiang-xi-tong-su-de-si-lu-fen-xi-duo-jie-fa-by-3-8/)***
