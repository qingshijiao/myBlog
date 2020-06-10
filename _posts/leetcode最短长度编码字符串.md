---
title: 471.最短长度编码字符串（Encode String with Shortest Length）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
Given a non-empty string, encode the string such that its encoded length is the shortest.

The encoding rule is: k[encoded_string], where the encoded_string inside the square brackets is being repeated exactly k times.

Note:
k will be a positive integer and encoded string will not be empty or have extra space.
You may assume that the input string contains only lowercase English letters. The string's length is at most 160.
If an encoding process does not make the string shorter, then do not encode it. If there are several solutions, return any of them is fine.
Example 1:

Input: "aaa"
Output: "aaa"
Explanation: There is no way to encode it such that it is shorter than the input string, so we do not encode it.
Example 2:

Input: "aaaaa"
Output: "5[a]"
Explanation: "5[a]" is shorter than "aaaaa" by 1 character.
Example 3:

Input: "aaaaaaaaaa"
Output: "10[a]"
Explanation: "a9[a]" or "9[a]a" are also valid solutions, both of them have the same length = 5, which is the same as "10[a]".
Example 4:

Input: "aabcaabcd"
Output: "2[aabc]d"
Explanation: "aabc" occurs twice, so one answer can be "2[aabc]d".
Example 5:

Input: "abbbabbbcabbbabbbc"
Output: "2[2[abbb]c]"
Explanation: "abbbabbbc" occurs twice, but "abbbabbbc" can also be encoded to "2[abbb]c", so one answer can be "2[2[abbb]c]".

#### Solution

Language: **c++**

```c++
class Solution {
public:
    string encode(string s) {
        int n = s.size();
        vector<vector<string>> dp(n, vector<string>(n, ""));
        for (int step = 1; step <= n; ++step) {
            for (int i = 0; i + step - 1 < n; ++i) {
                int j = i + step - 1;
                dp[i][j] = s.substr(i, step);
                string t = s.substr(i, j - i + 1), replace = "";
                auto pos = (t + t).find(t, 1);
                if (pos < t.size()) {
                    replace = to_string(t.size() / pos) + "[" + dp[i][i + pos - 1] + "]";
                    if (replace.size() < dp[i][j].size()) dp[i][j] = replace;
                    continue;
                }
                for (int k = i; k < j; ++k) {
                    string left = dp[i][k], right = dp[k + 1][j];
                    if (left.size() + right.size() < dp[i][j].size()) {
                        dp[i][j] = left + right;
                    }
                }
            }
        }
        return dp[0][n - 1];
    }
};
```


---
***参考：
[grandyang](https://www.cnblogs.com/grandyang/p/6194403.html)***
