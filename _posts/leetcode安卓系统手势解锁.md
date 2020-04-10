---
title: 351.安卓系统手势解锁 (Android Unlock Patterns)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### 题目描述
Given an Android 3x3 key lock screen and two integers m and n, where 1 ≤ m ≤ n ≤ 9, count the total number of unlock patterns of the Android lock screen, which consist of minimum of m keys and maximum n keys.



Rules for a valid pattern:

- Each pattern must connect at least m keys and at most n keys.
- All the keys must be distinct.
- If the line connecting two consecutive keys in the pattern passes through any other keys, the other keys must have previously selected in the pattern. No jumps through non selected key is allowed.
- The order of keys used matters.

![](https://assets.leetcode.com/uploads/2018/10/12/android-unlock.png)

Explanation:
```
| 1 | 2 | 3 |
| 4 | 5 | 6 |
| 7 | 8 | 9 |
Invalid move: 4 - 1 - 3 - 6
Line 1 - 3 passes through key 2 which had not been selected in the pattern.

Invalid move: 4 - 1 - 9 - 2
Line 1 - 9 passes through key 5 which had not been selected in the pattern.

Valid move: 2 - 4 - 1 - 3 - 6
Line 1 - 3 is valid because it passes through key 2, which had been selected in the pattern

Valid move: 6 - 5 - 4 - 1 - 9 - 2
Line 1 - 9 is valid because it passes through key 5, which had been selected in the pattern.
```


Example:
```
Input: m = 1, n = 1
Output: 9
```

#### Solution1

Language: **C++**

```c++
class Solution {
public:
    int numberOfPatterns(int m, int n) {
        int res = 0;
        vector<bool> visited(10, false);
        vector<vector<int>> jumps(10, vector<int>(10, 0));
        jumps[1][3] = jumps[3][1] = 2;
        jumps[4][6] = jumps[6][4] = 5;
        jumps[7][9] = jumps[9][7] = 8;
        jumps[1][7] = jumps[7][1] = 4;
        jumps[2][8] = jumps[8][2] = 5;
        jumps[3][9] = jumps[9][3] = 6;
        jumps[1][9] = jumps[9][1] = jumps[3][7] = jumps[7][3] = 5;
        res += helper(1, 1, m, n, jumps, visited, 0) * 4;
        res += helper(2, 1, m, n, jumps, visited, 0) * 4;
        res += helper(5, 1, m, n, jumps, visited, 0);
        return res;
    }
    int helper(int num, int len, int m, int n, vector<vector<int>>& jumps, vector<bool>& visited, int res) {
        if (len >= m) ++res;
        ++len;
        if (len > n) return res;
        visited[num] = true;
        for (int next = 1; next <= 9; ++next) {
            int jump = jumps[num][next];
            if (!visited[next] && (jump == 0 || visited[jump])) {
                res = helper(next, len, m, n, jumps, visited, res);
            }
        }
        visited[num] = false;
        return res;
    }
};
```

#### Solution2

Language: **C++**

```c++
class Solution {
public:
    int numberOfPatterns(int m, int n) {
        return count(m, n, 0, 1, 1);
    }
    int count(int m, int n, int used, int i1, int j1) {
        int res = m <= 0;
        if (!n) return 1;
        for (int i = 0; i < 3; ++i) {
            for (int j = 0; j < 3; ++j) {
                int I = i1 + i, J = j1 + j, used2 = used | (1 << (i * 3 + j));
                if (used2 > used && (I % 2 || J % 2 || used2 & (1 << (I / 2 * 3 + J / 2)))) {
                    res += count(m - 1, n - 1, used2, i, j);
                }
            }
        }
        return res;
    }
};
```


---
***参考:
[grandyang](https://www.cnblogs.com/grandyang/p/5541012.html)***
