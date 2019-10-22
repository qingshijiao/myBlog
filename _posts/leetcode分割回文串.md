---
title: 131.分割回文串（Palindrome Partitioning）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给定一个字符串 s，将 s 分割成一些子串，使每个子串都是回文串。

返回 s 所有可能的分割方案。

示例:
```
输入: "aab"
输出:
[
  ["aa","b"],
  ["a","a","b"]
]
```


# 题解

## 官方题解
暂无


## 其他题解

### 1.分治法
**思路：**


```
class Solution {
    public List<List<String>> partition(String s) {
        return partitionHelper(s, 0);
    }

    private List<List<String>> partitionHelper(String s, int start) {
        //递归出口，空字符串
        if (start == s.length()) {
            List<String> list = new ArrayList<>();
            List<List<String>> ans = new ArrayList<>();
            ans.add(list);
            return ans;
        }
        List<List<String>> ans = new ArrayList<>();
        for (int i = start; i < s.length(); i++) {
            //当前切割后是回文串才考虑
            if (isPalindrome(s.substring(start, i + 1))) {
                String left = s.substring(start, i + 1);
                //遍历后边字符串的所有结果，将当前的字符串加到头部
                for (List<String> l : partitionHelper(s, i + 1)) {
                    l.add(0, left);
                    ans.add(l);
                }
            }

        }
        return ans;
    }

    private boolean isPalindrome(String s) {
        int i = 0;
        int j = s.length() - 1;
        while (i < j) {
            if (s.charAt(i) != s.charAt(j)) {
                return false;
            }
            i++;
            j--;
        }
        return true;
    }

}
```

### 2.分治法优化
**思路：**


```
class Solution {
  public List<List<String>> partition(String s) {
    boolean[][] dp = new boolean[s.length()][s.length()];
    int length = s.length();
    for (int len = 1; len <= length; len++) {
        for (int i = 0; i <= s.length() - len; i++) {
            int j = i + len - 1;
            dp[i][j] = s.charAt(i) == s.charAt(j) && (len < 3 || dp[i + 1][j - 1]);
        }
    }
    return partitionHelper(s, 0, dp);
  }

  private List<List<String>> partitionHelper(String s, int start, boolean[][] dp) {
    if (start == s.length()) {
        List<String> list = new ArrayList<>();
        List<List<String>> ans = new ArrayList<>();
        ans.add(list);
        return ans;
    }
    List<List<String>> ans = new ArrayList<>();
    for (int i = start; i < s.length(); i++) {
        if (dp[start][i]) {
            String left = s.substring(start, i + 1);
            for (List<String> l : partitionHelper(s, i + 1, dp)) {
                l.add(0, left);
                ans.add(l);
            }
        }

    }
    return ans;
  }

}
```

### 3.回溯法
**思路：**

![](https://pic.leetcode-cn.com/3d757955a494533faaa83729fcd3be4d545438014018b70254655aa11ca794c9.jpg)

```
class Solution {
    public List<List<String>> partition(String s) {
        boolean[][] dp = new boolean[s.length()][s.length()];
        int length = s.length();
        for (int len = 1; len <= length; len++) {
            for (int i = 0; i <= s.length() - len; i++) {
                dp[i][i + len - 1] = s.charAt(i) == s.charAt(i + len - 1) && (len < 3 || dp[i + 1][i + len - 2]);
            }
        }
        List<List<String>> ans = new ArrayList<>();
        partitionHelper(s, 0, dp, new ArrayList<>(), ans);
        return ans;
    }

    private void partitionHelper(String s, int start, boolean[][] dp, List<String> temp, List<List<String>> res) {
        //到了空串就加到最终的结果中
        if (start == s.length()) {
            res.add(new ArrayList<>(temp));
        }
        //在不同位置切割
        for (int i = start; i < s.length(); i++) {
            //如果是回文串就加到结果中
            if (dp[start][i]) {
                String left = s.substring(start, i + 1);
                temp.add(left);
                partitionHelper(s, i + 1, dp, temp, res);
                temp.remove(temp.size() - 1);
            }

        }
    }

}
```

```
class Solution {
    public List<List<String>> partition(String s) {
        // validate
        if (null == s || 0 == s.length()) {
            return new ArrayList<>();
        }
        List<List<String>> res = new ArrayList<>();
        List<String> temp = new ArrayList<>();
        doPartition(s.toCharArray(),0,res,temp);
        return res;
    }

    private void doPartition(char[] chs,int start,List<List<String>> res,List<String> temp) {
        // base case
        if (start == chs.length) {
            res.add(new ArrayList<>(temp));
            return;
        }
        for (int i = start;i < chs.length;i++) {
            if (isPalindrome(chs,start,i)) {
                temp.add(new String(chs,start,i-start+1));
                doPartition(chs,i+1,res,temp);
                // recover
                temp.remove(temp.size()-1);
            }
        }
    }

    private boolean isPalindrome(char[] chs,int start,int end) {
        while (start < end) {
            if (chs[start] == chs[end]) {
                start++;
                end--;
            } else {
                return false;
            }
        }
        return true;
    }

}
```



---
***参考：
[LeetCode](https://leetcode-cn.com/problems/palindrome-partitioning/submissions/)
[windliang](https://leetcode-cn.com/problems/palindrome-partitioning/solution/xiang-xi-tong-su-de-si-lu-fen-xi-duo-jie-fa-by-3-7/)***
