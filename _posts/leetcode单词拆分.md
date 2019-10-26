---
title: 139.单词拆分（Word Break）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给定一个非空字符串 s 和一个包含非空单词列表的字典 wordDict，判定 s 是否可以被空格拆分为一个或多个在字典中出现的单词。

说明：

- 拆分时可以重复使用字典中的单词。
- 你可以假设字典中没有重复的单词。

示例 1：
```
输入: s = "leetcode", wordDict = ["leet", "code"]
输出: true
解释: 返回 true 因为 "leetcode" 可以被拆分成 "leet code"。
```
示例 2：
```
输入: s = "applepenapple", wordDict = ["apple", "pen"]
输出: true
解释: 返回 true 因为 "applepenapple" 可以被拆分成 "apple pen apple"。
     注意你可以重复使用字典中的单词。
```
示例 3：
```
输入: s = "catsandog", wordDict = ["cats", "dog", "sand", "and", "cat"]
输出: false
```

# 题解

## 官方题解
### 1.暴力法
**思路：** 最简单的实现方法是用递归和回溯。为了找到解，我们可以检查字典单词中每一个单词的可能前缀，如果在字典中出现过，那么去掉这个前缀后剩余部分回归调用。同时，如果某次函数调用中发现整个字符串都已经被拆分且在字典中出现过了，函数就返回 true 。


```
public class Solution {
    public boolean wordBreak(String s, List<String> wordDict) {
        return word_Break(s, new HashSet(wordDict), 0);
    }
    public boolean word_Break(String s, Set<String> wordDict, int start) {
        if (start == s.length()) {
            return true;
        }
        for (int end = start + 1; end <= s.length(); end++) {
            if (wordDict.contains(s.substring(start, end)) && word_Break(s, wordDict, end)) {
                return true;
            }
        }
        return false;
    }
}

```
**复杂度分析：**
- 时间复杂度：O(n^n)。考虑最坏情况 s = aaaaaaa 。每一个前缀都在字典中，此时回溯树的复杂度会达到 n^n。
- 空间复杂度：O(n^n)。回溯树的深度最深达到 n 。

### 2.记忆法回溯
**思路：** 通过记忆化，许多冗余的子问题可以极大被优化，回溯树得到了剪枝，因此极大减小了时间复杂度。


```
public class Solution {
    public boolean wordBreak(String s, List<String> wordDict) {
        return word_Break(s, new HashSet(wordDict), 0, new Boolean[s.length()]);
    }
    public boolean word_Break(String s, Set<String> wordDict, int start, Boolean[] memo) {
        if (start == s.length()) {
            return true;
        }
        if (memo[start] != null) {
            return memo[start];
        }
        for (int end = start + 1; end <= s.length(); end++) {
            if (wordDict.contains(s.substring(start, end)) && word_Break(s, wordDict, end, memo)) {
                return memo[start] = true;
            }
        }
        return memo[start] = false;
    }
}

```
**复杂度分析：**
- 时间复杂度：O(n^2)。回溯树的大小最多达到 n^2。
- 空间复杂度：O(n)。回溯树的深度可以达到 n 级别。

### 3.宽度优先遍历
**思路：** 另一个方法是使用宽度优先搜索。将字符串可视化成一棵树，每一个节点是用 endend 为结尾的前缀字符串。当两个节点之间的所有节点都对应了字典中一个有效字符串时，两个节点可以被连接。

![](https://pic.leetcode-cn.com/13748edb1a2cab3f7636a0af409de256aa1048ff976dff44627c118b9f9b5fbb-image.png)


```
public class Solution {
    public boolean wordBreak(String s, List<String> wordDict) {
        Set<String> wordDictSet=new HashSet(wordDict);
        Queue<Integer> queue = new LinkedList<>();
        int[] visited = new int[s.length()];
        queue.add(0);
        while (!queue.isEmpty()) {
            int start = queue.remove();
            if (visited[start] == 0) {
                for (int end = start + 1; end <= s.length(); end++) {
                    if (wordDictSet.contains(s.substring(start, end))) {
                        queue.add(end);
                        if (end == s.length()) {
                            return true;
                        }
                    }
                }
                visited[start] = 1;
            }
        }
        return false;
    }
}
```
**复杂度分析：**
- 时间复杂度：O(n^2)。对于每个开始的位置，搜索会直到给定字符串的尾部结束。
- 空间复杂度：O(n)。队列的大小最多 n。

### 4.动态规划
**思路：**


```
public class Solution {
    public boolean wordBreak(String s, List<String> wordDict) {
        Set<String> wordDictSet=new HashSet(wordDict);
        boolean[] dp = new boolean[s.length() + 1];
        dp[0] = true;
        for (int i = 1; i <= s.length(); i++) {
            for (int j = 0; j < i; j++) {
                if (dp[j] && wordDictSet.contains(s.substring(j, i))) {
                    dp[i] = true;
                    break;
                }
            }
        }
        return dp[s.length()];
    }
}
```
```
class Solution {
    public boolean wordBreak(String s, List<String> wordDict) {
        int m = s.length();
        boolean[] canSegment = new boolean[m + 1];
        canSegment[0] = true;
        int maxLength = getMaxLength(wordDict);
        for(int i=1; i < m + 1; i++){
            canSegment[i] = false;
            for(int lastWordLength = 1;
               lastWordLength <= maxLength && lastWordLength <= i;
               lastWordLength++){
                if(!canSegment[i - lastWordLength]){
                    continue;
                }
                String word = s.substring(i - lastWordLength, i);
                if(wordDict.contains(word)){
                    canSegment[i] = true;
                    break;
                }
            }
        }
        return canSegment[m];
    }
    private int getMaxLength(List<String> wordDict){
        int maxLength = 0;
        for(String word : wordDict){
            maxLength = Math.max(maxLength, word.length());
        }
        return maxLength;
    }
}
```

**复杂度分析：**
- 时间复杂度：O(n^2)。求出 dp 数组需要两重循环。
- 空间复杂度：O(n)。dp 数组的长度是 n+1。


## 其他题解
暂无

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/word-break/solution/dan-ci-chai-fen-by-leetcode/)***
