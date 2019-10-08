---
title: 97.交错字符串（Interleaving String）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给定三个字符串 s1, s2, s3, 验证 s3 是否是由 s1 和 s2 交错组成的。

示例 1:
```
输入: s1 = "aabcc", s2 = "dbbca", s3 = "aadbbcbcac"
输出: true
```
示例 2:
```
输入: s1 = "aabcc", s2 = "dbbca", s3 = "aadbbbaccc"
输出: false
```


# 题解

## 官方题解
### 1.递归
**思路：**
```
s1="abc"
s2="bcd"
s3="abcbdc"
```
首先，我们选择 s1 字符串的第一个字母 'a' ，所以递归进去后， s1 变为 "bc" ， s2 保持不变为 "bcd" ，s3s3 为 "abcbdc" 。当函数返回结果的时候，我们再次调用递归函数，但是这次 3 个字符串分别变为 s1="abc" ， s2="cd" ，s3="abcbdc" 。


```
public class Solution {
    public boolean is_Interleave(String s1,int i,String s2,int j,String res,String s3)
    {
        if(res.equals(s3) && i==s1.length() && j==s2.length())
            return true;
        boolean ans=false;
        if(i<s1.length())
            ans|=is_Interleave(s1,i+1,s2,j,res+s1.charAt(i),s3);
        if(j<s2.length())
            ans|=is_Interleave(s1,i,s2,j+1,res+s2.charAt(j),s3);
        return ans;

    }
    public boolean isInterleave(String s1, String s2, String s3) {
        return is_Interleave(s1,0,s2,0,"",s3);
    }
}

```

**复杂度分析**
- 时间复杂度：O(2^(m+n))。 m 是 s1 的长度， n 是 s2 的长度。
- 空间复杂度：O(m+n) 。递归栈的深度最多为 m+n 。

### 2.记忆法递归
**思路：**

```
public class Solution {
   public boolean is_Interleave(String s1, int i, String s2, int j, String s3, int k, int[][] memo) {
       if (i == s1.length()) {
           return s2.substring(j).equals(s3.substring(k));
       }
       if (j == s2.length()) {
           return s1.substring(i).equals(s3.substring(k));
       }
       if (memo[i][j] >= 0) {
           return memo[i][j] == 1 ? true : false;
       }
       boolean ans = false;
       if (s3.charAt(k) == s1.charAt(i) && is_Interleave(s1, i + 1, s2, j, s3, k + 1, memo)
               || s3.charAt(k) == s2.charAt(j) && is_Interleave(s1, i, s2, j + 1, s3, k + 1, memo)) {
           ans = true;
       }
       memo[i][j] = ans ? 1 : 0;
       return ans;
   }
   public boolean isInterleave(String s1, String s2, String s3) {
       int memo[][] = new int[s1.length()][s2.length()];
       for (int i = 0; i < s1.length(); i++) {
           for (int j = 0; j < s2.length(); j++) {
               memo[i][j] = -1;
           }
       }
       return is_Interleave(s1, 0, s2, 0, s3, 0, memo);
   }
}

```

**复杂度分析**
- 时间复杂度：O(2^(m+n))。 m 是 s1 的长度， n 是 s2 的长度。
- 空间复杂度：O(m+n) 。记忆化数组需要 m * n 的空间。

### 3.使用二维动态规划
**思路：**
```
s1="aabcc"
s2="dbbca"
s3="aadbbcbcac"
```

![](https://pic.leetcode-cn.com/617399ffd2e766b27898847c9941dae3dc1a82ccfe8123cb4590bfe9518b7cf7-image.png)
![](https://pic.leetcode-cn.com/f0e37131f6b1a374317d9f2a875054610bfc00721f9f5d2b426348978b0a3bc8-image.png)
![](https://pic.leetcode-cn.com/5c311949beb71b1c96691a8fd21d45b0a7f10bf82aba3f24de4c70bb33eee991-image.png)
![](https://pic.leetcode-cn.com/a046049f67a51c94107a314ddeda6ac731c5380fa09a59357ea8d4272e2fd278-image.png)
![](https://pic.leetcode-cn.com/1ea87cbbf785bc31fbc4f10349545947a3bd7dd5c182ca7d038b054b2577e8e2-image.png)

```
public class Solution {
    public boolean isInterleave(String s1, String s2, String s3) {
        if (s3.length() != s1.length() + s2.length()) {
            return false;
        }
        boolean dp[][] = new boolean[s1.length() + 1][s2.length() + 1];
        for (int i = 0; i <= s1.length(); i++) {
            for (int j = 0; j <= s2.length(); j++) {
                if (i == 0 && j == 0) {
                    dp[i][j] = true;
                } else if (i == 0) {
                    dp[i][j] = dp[i][j - 1] && s2.charAt(j - 1) == s3.charAt(i + j - 1);
                } else if (j == 0) {
                    dp[i][j] = dp[i - 1][j] && s1.charAt(i - 1) == s3.charAt(i + j - 1);
                } else {
                    dp[i][j] = (dp[i - 1][j] && s1.charAt(i - 1) == s3.charAt(i + j - 1)) || (dp[i][j - 1] && s2.charAt(j - 1) == s3.charAt(i + j - 1));
                }
            }
        }
        return dp[s1.length()][s2.length()];
    }
}
```

**复杂度分析**
- 时间复杂度：O(m⋅n) 。计算 dp 数组需要 m*n 的时间。
- 空间复杂度：O(m⋅n)。2 维的 dp 数组需要 (m+1)*(n+1) 的空间。 m 和 n 分别是 s1 和 s2 字符串的长度。

### 4.使用一维动态规划
**思路：**

```
public class Solution {
   public boolean isInterleave(String s1, String s2, String s3) {
       if (s3.length() != s1.length() + s2.length()) {
           return false;
       }
       boolean dp[] = new boolean[s2.length() + 1];
       for (int i = 0; i <= s1.length(); i++) {
           for (int j = 0; j <= s2.length(); j++) {
               if (i == 0 && j == 0) {
                   dp[j] = true;
               } else if (i == 0) {
                   dp[j] = dp[j - 1] && s2.charAt(j - 1) == s3.charAt(i + j - 1);
               } else if (j == 0) {
                   dp[j] = dp[j] && s1.charAt(i - 1) == s3.charAt(i + j - 1);
               } else {
                   dp[j] = (dp[j] && s1.charAt(i - 1) == s3.charAt(i + j - 1)) || (dp[j - 1] && s2.charAt(j - 1) == s3.charAt(i + j - 1));
               }
           }
       }
       return dp[s2.length()];
   }
}

```

**复杂度分析**
- 时间复杂度：O(m⋅n)；长度为 n 的 dp 数组需要被填充 m 次。
- 空间复杂度：O(n)；n 是字符串 s1 的长度




## 其他题解
### 1.BFS
**思路：**

```
class Solution {
    public boolean isInterleave(String s1, String s2, String s3) {
        int n1 = s1.length();
        int n2 = s2.length();
        int n3 = s3.length();
        if (n1 + n2 != n3) return false;
        boolean[][] visited = new boolean[n1 + 1][n2 + 1];
        Queue<int[]> queue = new LinkedList<>();
        queue.offer(new int[]{0, 0});
        while (!queue.isEmpty()) {
            int[] tmp = queue.poll();
            if (tmp[0] == n1 && tmp[1] == n2) return true;
            if (tmp[0] < n1 && s1.charAt(tmp[0]) == s3.charAt(tmp[0] + tmp[1]) && !visited[tmp[0] + 1][tmp[1]]) {
                visited[tmp[0] + 1][tmp[1]] = true;
                queue.offer(new int[]{tmp[0] + 1, tmp[1]});
            }
            if (tmp[1] < n2 && s2.charAt(tmp[1]) == s3.charAt(tmp[0] + tmp[1]) && !visited[tmp[0]][tmp[1] + 1]) {
                visited[tmp[0]][tmp[1] + 1] = true;
                queue.offer(new int[]{tmp[0], tmp[1] + 1});
            }

        }
        return false;
    }
}

```


---
***参考：
[LeetCode](https://leetcode-cn.com/problems/interleaving-string/solution/jiao-cuo-zi-fu-chuan-by-leetcode/)
[powcai](https://leetcode-cn.com/problems/interleaving-string/solution/dong-tai-gui-hua-he-bfs-by-powcai/)***
