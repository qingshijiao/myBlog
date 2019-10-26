---
title: 140.单词拆分 II（Word Break II）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给定一个非空字符串 s 和一个包含非空单词列表的字典 wordDict，在字符串中增加空格来构建一个句子，使得句子中所有的单词都在词典中。返回所有这些可能的句子。

说明：

- 分隔时可以重复使用字典中的单词。
- 你可以假设字典中没有重复的单词。

示例 1：
```
输入:
s = "catsanddog"
wordDict = ["cat", "cats", "and", "sand", "dog"]
输出:
[
  "cats and dog",
  "cat sand dog"
]
```
示例 2：
```
输入:
s = "pineapplepenapple"
wordDict = ["apple", "pen", "applepen", "pine", "pineapple"]
输出:
[
  "pine apple pen apple",
  "pineapple pen apple",
  "pine applepen apple"
]
解释: 注意你可以重复使用字典中的单词。
```
示例 3：
```
输入:
s = "catsandog"
wordDict = ["cats", "dog", "sand", "and", "cat"]
输出:
[]
```


# 题解

## 官方题解
### 1.暴力法
**思路：** 解决此题最简单的方法是使用回溯。为了找到解，我们检查字符串（s）的所有可能前缀是否在字典中，如果在（比方说 s1 ），那么调用回溯函数并检查剩余部分的字符串。



```
class Solution {
    public List<String> wordBreak(String s, List<String> wordDict) {
            return word_Break(s, wordDict, 0);
    }
    public List<String> word_Break(String s, List<String> wordDict, int start) {
        LinkedList<String> res = new LinkedList<>();
        if (start == s.length()) {
            res.add("");
        }
        for (int end = start + 1; end <= s.length(); end++) {
            if (wordDict.contains(s.substring(start, end))) {
                List<String> list = word_Break(s, wordDict, end);
                for (String l : list) {
                    res.add(s.substring(start, end) + (l.equals("") ? "" : " ") + l);
                }
            }
        }
        return res;
    }

}

```
**复杂度分析：**
- 时间复杂度：O(n^n)。考虑最坏情况 s = aaaaaaa 。每一个前缀都在字典中，此时回溯树的复杂度会达到 n^n。
- 空间复杂度：O(n^3)。最坏情况下，回溯的深度可以达到 n 层，每层可能包含 n 个字符串，且每个字符串的长度都为 n 。



### 2.记忆法回溯
**思路：** 通过记忆化，许多冗余的子问题可以极大被优化，回溯树得到了剪枝，因此极大减小了时间复杂度。


```
class Solution {
    public List<String> wordBreak(String s, List<String> wordDict) {
        return word_Break(s, wordDict, 0);
    }
    HashMap<Integer, List<String>> map = new HashMap<>();

    public List<String> word_Break(String s, List<String> wordDict, int start) {
        if (map.containsKey(start)) {
            return map.get(start);
        }
        LinkedList<String> res = new LinkedList<>();
        if (start == s.length()) {
            res.add("");
        }
        for (int end = start + 1; end <= s.length(); end++) {
            if (wordDict.contains(s.substring(start, end))) {
                List<String> list = word_Break(s, wordDict, end);
                for (String l : list) {
                    res.add(s.substring(start, end) + (l.equals("") ? "" : " ") + l);
                }
            }
        }
        map.put(start, res);
        return res;
    }

}

```

```
class Solution {
    public List<String> getWordBreak(String s, List<String> wordDict, HashMap<String, List<String>> cache) {

        if (cache.containsKey(s)) return cache.get(s);

        List<String> res = new ArrayList<>();

        if (s.length() == 0) {
            res.add("");
            return res;
        }

        List<String> subRes;
        for (String str : wordDict) {
            if (s.endsWith(str))  {

                String newString = s.substring(0, s.length() - str.length());
                subRes = getWordBreak(newString, wordDict, cache);

                for (int i = 0; i < subRes.size(); i++) {
                    if (subRes.get(i).equals("")) res.add(str);
                    else res.add(subRes.get(i) + " " + str);
                }
            }
        }

        cache.put(s, res);
        return res;
    }

    public List<String> wordBreak(String s, List<String> wordDict) {

        HashMap<String, List<String>> cache = new HashMap<>();
        return getWordBreak(s, wordDict, cache);
    }
}
```

**复杂度分析：**
- 时间复杂度：O(n^3)。回溯树的大小最多达到 n^2。创建列表需要 n 的时间。


### 3.动态规划
**思路：**

```
public class Solution {
   public List<String> wordBreak(String s, Set<String> wordDict) {
       LinkedList<String>[] dp = new LinkedList[s.length() + 1];
       LinkedList<String> initial = new LinkedList<>();
       initial.add("");
       dp[0] = initial;
       for (int i = 1; i <= s.length(); i++) {
           LinkedList<String> list = new LinkedList<>();
           for (int j = 0; j < i; j++) {
               if (dp[j].size() > 0 && wordDict.contains(s.substring(j, i))) {
                   for (String l : dp[j]) {
                       list.add(l + (l.equals("") ? "" : " ") + s.substring(j, i));
                   }
               }
           }
           dp[i] = list;
       }
       return dp[s.length()];
   }
}

```
**复杂度分析：**
- 时间复杂度：O(n^3)。求 dp 需要两重循环，添加一个新的列表需要额外一重循环。
- 空间复杂度：O(n^3)。dp 数组的长度是 n， dp 数组里保存了数组，数组里是一些字符串，也就是每个 dp 元素需要 n^2的空间。



## 其他题解
### 1.DFS
**思路：**

```
class Solution {
   public List<String> wordBreak(String s, List<String> wordDict) {
        Set<String> set = new HashSet<String>(wordDict);
        List<String> res = new ArrayList<String>();
        int length = s.length();
        boolean[] dp = new boolean[length + 1];
        int max = Integer.MIN_VALUE;
        int min = Integer.MAX_VALUE;
        int len = 0;

        for (String tmp : wordDict) {
            len = tmp.length();
            if (len > max) {
                max = len;
            }
            if (len < min) {
                min = len;
            }
        }

        dp[0] = true;
        for (int i = min; i <= length; i++) {
            for (int j = i - min; j >= i - max && j >= 0; j--) {
                if (dp[j] && set.contains(s.substring(j, i))) {
                    dp[i] = true;
                    break;
                }
            }
        }

        if (!dp[length]) {
            return res;
        }

        StringBuilder sb = new StringBuilder();
        dfs(s, set, sb, res, 0);
        return res;

    }

    public void dfs(String s, Set<String> wordDict, StringBuilder sb, List<String> res, int start) {
        if (start == s.length()) {
            res.add(sb.toString().trim());
            return;
        }

        for (int i = start; i < s.length(); i++) {
            String str = s.substring(start, i + 1);
            if (wordDict.contains(str)) {
                int length = sb.length();
                sb.append(str).append(" ");
                dfs(s, wordDict, sb, res, i + 1);
                sb.setLength(length);
            }
        }
    }
}
```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/word-break-ii/solution/dan-ci-chai-fen-ii-by-leetcode/)***
