---
title: 115.不同的子序列（Distinct Subsequences）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给定一个字符串 S 和一个字符串 T，计算在 S 的子序列中 T 出现的个数。

一个字符串的一个子序列是指，通过删除一些（也可以不删除）字符且不干扰剩余字符相对位置所组成的新字符串。（例如，"ACE" 是 "ABCDE" 的一个子序列，而 "AEC" 不是）

示例 1:
```
输入: S = "rabbbit", T = "rabbit"
输出: 3
解释:

如下图所示, 有 3 种可以从 S 中得到 "rabbit" 的方案。
(上箭头符号 ^ 表示选取的字母)

rabbbit
^^^^ ^^
rabbbit
^^ ^^^^
rabbbit
^^^ ^^^
```
示例 2:
```
输入: S = "babgbag", T = "bag"
输出: 5
解释:

如下图所示, 有 5 种可以从 S 中得到 "bag" 的方案。
(上箭头符号 ^ 表示选取的字母)

babgbag
^^ ^
babgbag
^^    ^
babgbag
^    ^^
babgbag
  ^  ^^
babgbag
    ^^^
```


# 题解

## 官方题解
暂无

## 其他题解
### 1.递归 - 分治
**思路：**
```
class Solution {
    public int numDistinct(String s, String t) {
        HashMap<String, Integer> map = new HashMap<>();
        return numDistinctHelper(s, 0, t, 0, map);
    }

    private int numDistinctHelper(String s, int s_start, String t, int t_start, HashMap<String, Integer> map) {
        //T 是空串，选法就是 1 种
        if (t_start == t.length()) {
            return 1;
        }
        //S 是空串，选法是 0 种
        if (s_start == s.length()) {
            return 0;
        }
        String key = s_start + "@" + t_start;
        //先判断之前有没有求过这个解
        if (map.containsKey(key)) {
            return map.get(key);
        }
        int count = 0;
        //当前字母相等
        if (s.charAt(s_start) == t.charAt(t_start)) {
            //从 S 选择当前的字母，此时 S 跳过这个字母, T 也跳过一个字母。
            count = numDistinctHelper(s, s_start + 1, t, t_start + 1, map)
            //S 不选当前的字母，此时 S 跳过这个字母，T 不跳过字母。
                  + numDistinctHelper(s, s_start + 1, t, t_start, map);
        //当前字母不相等
        }else{
            //S 只能不选当前的字母，此时 S 跳过这个字母， T 不跳过字母。
            count = numDistinctHelper(s, s_start + 1, t, t_start, map);
        }
        //将当前解放到 map 中
        map.put(key, count);
        return count;
    }

}

```


### 2.递归 - 回溯
**思路：**

```
class Solution {
    int count = 0;
    public int numDistinct(String s, String t) {
        HashMap<String, Integer> map = new HashMap<>();
        numDistinctHelper(s, 0, t, 0, map);
        return count;
    }

    private void numDistinctHelper(String s, int s_start, String t, int t_start,
                HashMap<String, Integer> map) {
        if (t_start == t.length()) {
            count++;
            return;
        }
        if (s_start == s.length()) {
            return;
        }
        String key = s_start + "@" + t_start;
        if (map.containsKey(key)) {
            count += map.get(key);
            return;
        }
        int count_pre = count;
        //当前字母相等，s_start 后移一个，t_start 后移一个
        if (s.charAt(s_start) == t.charAt(t_start)) {
            numDistinctHelper(s, s_start + 1, t, t_start + 1, map);
        }
        //出来以后，继续尝试不选择当前字母，s_start 后移一个，t_start 不后移
        numDistinctHelper(s, s_start + 1, t, t_start, map);

        //将增量存起来
        int count_increment = count - count_pre;
        map.put(key, count_increment);
    }

}

```

### 3.动态规划 - 二维
**思路：**
![](https://pic.leetcode-cn.com/6d72552b63811c20536fa2393c18a521fa5850657f87221678f4eba1b177cbbb.jpg)

```
class Solution {
    public int numDistinct(String s, String t) {
        int s_len = s.length();
        int t_len = t.length();
        int[][] dp = new int[s_len + 1][t_len + 1];
        //当 T 为空串时，所有的 s 对应于 1
        for (int i = 0; i <= s_len; i++) {
            dp[i][t_len] = 1;
        }

        //倒着进行，T 每次增加一个字母
        for (int t_i = t_len - 1; t_i >= 0; t_i--) {
            dp[s_len][t_i] = 0; // 这句可以省去，因为默认值是 0
            //倒着进行，S 每次增加一个字母
            for (int s_i = s_len - 1; s_i >= 0; s_i--) {
                //如果当前字母相等
                if (t.charAt(t_i) == s.charAt(s_i)) {
                    //对应于两种情况，选择当前字母和不选择当前字母
                    dp[s_i][t_i] = dp[s_i + 1][t_i + 1] + dp[s_i + 1][t_i];
                //如果当前字母不相等
                } else {
                    dp[s_i][t_i] = dp[s_i + 1][t_i];
                }
            }
        }
        return dp[0][0];
    }
}

```

## 4.递归 - 一维
**思路：**

```
public int numDistinct(String s, String t) {
    int s_len = s.length();
    int t_len = t.length();
    int[]dp = new int[s_len + 1];
    for (int i = 0; i <= s_len; i++) {
        dp[i] = 1;
    }
  //倒着进行，T 每次增加一个字母
    for (int t_i = t_len - 1; t_i >= 0; t_i--) {
        int pre = dp[s_len];
        dp[s_len] = 0;
         //倒着进行，S 每次增加一个字母
        for (int s_i = s_len - 1; s_i >= 0; s_i--) {
            int temp = dp[s_i];
            if (t.charAt(t_i) == s.charAt(s_i)) {
                dp[s_i] = dp[s_i + 1] + pre;
            } else {
                dp[s_i] = dp[s_i + 1];
            }
            pre = temp;
        }
    }
    return dp[0];
}
```

```
public int numDistinct(String s, String t) {
    int s_len = s.length();
    int t_len = t.length();
    int[] dp = new int[s_len + 1];
    for (int i = 0; i <= s_len; i++) {
        dp[i] = 1;
    }
    for (int t_i = 1; t_i <= t_len; t_i++) {
        int pre = dp[0];
        dp[0] = 0;
        for (int s_i = 1; s_i <= s_len; s_i++) {
            int temp = dp[s_i];
            if (t.charAt(t_i - 1) == s.charAt(s_i - 1)) {
                dp[s_i] = dp[s_i - 1] + pre;
            } else {
                dp[s_i] = dp[s_i - 1];
            }
            pre = temp;
        }
    }
    return dp[s_len];
}
```


---
***参考：
[LeetCode](https://leetcode-cn.com/problems/distinct-subsequences/submissions/)
[windliang](https://leetcode-cn.com/problems/distinct-subsequences/solution/xiang-xi-tong-su-de-si-lu-fen-xi-duo-jie-fa-by-27/)***
