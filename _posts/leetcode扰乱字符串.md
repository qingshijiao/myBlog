---
title: 87.扰乱字符串（Scramble String）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给定一个字符串 s1，我们可以把它递归地分割成两个非空子字符串，从而将其表示为二叉树。

下图是字符串 s1 = "great" 的一种可能的表示形式。
```
    great
   /    \
  gr    eat
 / \    /  \
g   r  e   at
           / \
          a   t

```
在扰乱这个字符串的过程中，我们可以挑选任何一个非叶节点，然后交换它的两个子节点。

例如，如果我们挑选非叶节点 "gr" ，交换它的两个子节点，将会产生扰乱字符串 "rgeat" 。
```
    rgeat
   /    \
  rg    eat
 / \    /  \
r   g  e   at
           / \
          a   t

```
我们将 "rgeat” 称作 "great" 的一个扰乱字符串。

同样地，如果我们继续交换节点 "eat" 和 "at" 的子节点，将会产生另一个新的扰乱字符串 "rgtae" 。
```
    rgtae
   /    \
  rg    tae
 / \    /  \
r   g  ta  e
       / \
      t   a

```
我们将 "rgtae” 称作 "great" 的一个扰乱字符串。

给出两个长度相等的字符串 s1 和 s2，判断 s2 是否是 s1 的扰乱字符串。

示例 1:
```
输入: s1 = "great", s2 = "rgeat"
输出: true
```
示例 2:
```
输入: s1 = "abcde", s2 = "caebd"
输出: false
```


# 题解

## 官方题解
暂无


## 其他题解
### 1.暴力递归
**思路：**
- S1 切割为两部分，然后进行若干步切割交换，最后判断两个子树分别是否能变成 S2 的两部分。

![](https://pic.leetcode-cn.com/ef39a914e75aca14ff8cccd63f5b44f0433aa2c1a86cbf48a5e5b8bcc983bbfd-image.png)

- S1 切割并且交换为两部分，然后进行若干步切割交换，最后判断两个子树是否能变成 S2 的两部分。

![](https://pic.leetcode-cn.com/a3d78b8a49da53e09fd57f7baeb66958f55d755a317d540b7c2d156a82f876d7-image.png)

```
class Solution {
    public boolean isScramble(String s1, String s2) {
        if (s1.length() != s2.length()) {
            return false;
        }
        if (s1.equals(s2)) {
            return true;
        }

        //判断两个字符串每个字母出现的次数是否一致
        int[] letters = new int[26];
        for (int i = 0; i < s1.length(); i++) {
            letters[s1.charAt(i) - 'a']++;
            letters[s2.charAt(i) - 'a']--;
        }
        //如果两个字符串的字母出现不一致直接返回 false
        for (int i = 0; i < 26; i++) {
            if (letters[i] != 0) {
                return false;
            }
        }

        //遍历每个切割位置
        for (int i = 1; i < s1.length(); i++) {
            //对应情况 1 ，判断 S1 的子树能否变为 S2 相应部分
            if (isScramble(s1.substring(0, i), s2.substring(0, i)) && isScramble(s1.substring(i), s2.substring(i))) {
                return true;
            }
            //对应情况 2 ，S1 两个子树先进行了交换，然后判断 S1 的子树能否变为 S2 相应部分
            if (isScramble(s1.substring(i), s2.substring(0, s2.length() - i)) &&
               isScramble(s1.substring(0, i), s2.substring(s2.length() - i)) ) {
                return true;
            }
        }
        return false;
    }

}
```
**复杂度分析：**
- 时间复杂度：
- 空间复杂度：


### 2.记忆递归
**思路：**

```
class Solution {
    public boolean isScramble(String s1, String s2) {
        HashMap<String, Integer> memoization = new HashMap<>();
        return isScrambleRecursion(s1, s2, memoization);
    }

    public boolean isScrambleRecursion(String s1, String s2, HashMap<String, Integer> memoization) {
    	//判断之前是否已经有了结果
		int ret = memoization.getOrDefault(s1 + "#" + s2, -1);
		if (ret == 1) {
			return true;
		} else if (ret == 0) {
			return false;
		}
		if (s1.length() != s2.length()) {
			memoization.put(s1 + "#" + s2, 0);
			return false;
		}
		if (s1.equals(s2)) {
			memoization.put(s1 + "#" + s2, 1);
			return true;
		}

		int[] letters = new int[26];
		for (int i = 0; i < s1.length(); i++) {
			letters[s1.charAt(i) - 'a']++;
			letters[s2.charAt(i) - 'a']--;
		}
		for (int i = 0; i < 26; i++)
			if (letters[i] != 0) {
				memoization.put(s1 + "#" + s2, 0);
				return false;
			}

		for (int i = 1; i < s1.length(); i++) {
			if (isScramble(s1.substring(0, i), s2.substring(0, i)) && isScramble(s1.substring(i), s2.substring(i))) {
				memoization.put(s1 + "#" + s2, 1);
				return true;
			}
			if (isScramble(s1.substring(0, i), s2.substring(s2.length() - i))
					&& isScramble(s1.substring(i), s2.substring(0, s2.length() - i))) {
				memoization.put(s1 + "#" + s2, 1);
				return true;
			}
		}
		memoization.put(s1 + "#" + s2, 0);
		return false;
	}
}
```
**复杂度分析：**
- 时间复杂度：
- 空间复杂度：

### 3.动态规划
**思路：**
![](https://pic.leetcode-cn.com/4e0be1c5fd379b99b47ea802f208c6e1347945c569d5ccebf1ff8c105c1c326d-image.png)

![](https://pic.leetcode-cn.com/5773a68718e82af5c7e0cff25d093cb10cd0433aa63e02582dd5ec50d5088a9a-image.png)

```
class Solution {
    public boolean isScramble(String s1, String s2) {
        if (s1.length() != s2.length()) {
            return false;
        }
        if (s1.equals(s2)) {
            return true;
        }

        int[] letters = new int[26];
        for (int i = 0; i < s1.length(); i++) {
            letters[s1.charAt(i) - 'a']++;
            letters[s2.charAt(i) - 'a']--;
        }
        for (int i = 0; i < 26; i++) {
            if (letters[i] != 0) {
                return false;
            }
        }

        int length = s1.length();
        boolean[][][] dp = new boolean[length + 1][length][length];
        //遍历所有的字符串长度
        for (int len = 1; len <= length; len++) {
            //S1 开始的地方
            for (int i = 0; i + len <= length; i++) {
                //S2 开始的地方
                for (int j = 0; j + len <= length; j++) {
                    //长度是 1 无需切割
                    if (len == 1) {
                        dp[len][i][j] = s1.charAt(i) == s2.charAt(j);
                    } else {
                        //遍历切割后的左半部分长度
                        for (int q = 1; q < len; q++) {
                            dp[len][i][j] = dp[q][i][j] && dp[len - q][i + q][j + q]
                                || dp[q][i][j + len - q] && dp[len - q][i + q][j];
                            //如果当前是 true 就 break，防止被覆盖为 false
                            if (dp[len][i][j]) {
                                break;
                            }
                        }
                    }
                }
            }
        }
        return dp[length][0][0];
    }
}
```
**复杂度分析：**
- 时间复杂度：
- 空间复杂度：


---
***参考：
[LeetCode](https://leetcode-cn.com/problems/scramble-string/submissions/)
[windliang](https://leetcode-cn.com/problems/scramble-string/solution/xiang-xi-tong-su-de-si-lu-fen-xi-duo-jie-fa-by-1-2/)***
