---
title: 488. 祖玛游戏 (Zuma Game)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [488\. 祖玛游戏](https://leetcode-cn.com/problems/zuma-game/)

Difficulty: **困难**


回忆一下祖玛游戏。现在桌上有一串球，颜色有红色(R)，黄色(Y)，蓝色(B)，绿色(G)，还有白色(W)。 现在你手里也有几个球。

每一次，你可以从手里的球选一个，然后把这个球插入到一串球中的某个位置上（包括最左端，最右端）。接着，如果有出现三个或者三个以上颜色相同的球相连的话，就把它们移除掉。重复这一步骤直到桌上所有的球都被移除。

找到插入并可以移除掉桌上所有球所需的最少的球数。如果不能移除桌上所有的球，输出 -1 。

```
示例:
输入: "WRRBBW", "RB" 
输出: -1 
解释: WRRBBW -> WRR[R]BBW -> WBBW -> WBB[B]W -> WW （翻译者标注：手上球已经用完，桌上还剩两个球无法消除，返回-1）

输入: "WWRRBBWW", "WRBRW" 
输出: 2 
解释: WWRRBBWW -> WWRR[R]BBWW -> WWBBWW -> WWBB[B]WW -> WWWW -> empty

输入:"G", "GGGGG" 
输出: 2 
解释: G -> G[G] -> GG[G] -> empty 

输入: "RBYYBBRRB", "YRBGB" 
输出: 3 
解释: RBYYBBRRB -> RBYY[Y]BBRRB -> RBBBRRB -> RRRB -> B -> B[B] -> BB[B] -> empty 
```

**标注:**

1.  你可以假设桌上一开始的球中，不会有三个及三个以上颜色相同且连着的球。
2.  桌上的球不会超过20个，输入的数据中代表这些球的字符串的名字是 "board" 。
3.  你手中的球不会超过5个，输入的数据中代表这些球的字符串的名字是 "hand"。
4.  输入的两个字符串均为非空字符串，且只包含字符 'R','Y','B','G','W'。


#### Solution

Language: **java**

```java
​class Solution {
    private int length;
    private int[] boards;
    private int[] hands;

    private int hash(char ch) {
        switch (ch) {
            case 'R':
                return 0;
            case 'Y':
                return 1;
            case 'B':
                return 2;
            case 'G':
                return 3;
            case 'W':
                return 4;
        }
        return -1;
    }

    private int dfs(int left, int right, int k) {
        if (right < left || right >= length || left < 0) {
            return 0;
        }
        int res = Integer.MAX_VALUE;
        hands[boards[left]] -= k >= 2 ? 0 : 2 - k;
        if (hands[boards[left]] >= 0) {
            int p = dfs(left + 1, right, 0);
            if (p != -1) {
                res = k >= 2 ? 0 : 2 - k;
                res += p;
            }
        }
        hands[boards[left]] += k >= 2 ? 0 : 2 - k;
        for (int i = left + 1; i <= right; i++) {
            if (boards[i] == boards[left]) {
                int p1 = dfs(left + 1, i - 1, 0);
                if (p1 == -1) {
                    continue;
                }
                int p2 = dfs(i, right, k + 1);
                if (p2 == -1) {
                    continue;
                }
                res = Math.min(res, p1 + p2);
            }
        }
        return res == Integer.MAX_VALUE ? -1 : res;
    }

    public int findMinStep(String board, String hand) {
        length = board.length();
        hands = new int[5];
        for (int i = 0; i < hand.length(); i++) {
            hands[hash(hand.charAt(i))]++;
        }
        boards = new int[length];
        for (int i = 0; i < length; i++) {
            boards[i] = hash(board.charAt(i));
        }
        return dfs(0, length - 1, 0);
    }
}
```

---
***参考:
[leetcode](https://leetcode-cn.com/problems/zuma-game/submissions/)***
