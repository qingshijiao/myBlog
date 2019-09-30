---
title: 76. 最小覆盖子串（Minimum Window Substring）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给你一个字符串 S、一个字符串 T，请在字符串 S 里面找出：包含 T 所有字母的最小子串。

示例：
```
输入: S = "ADOBECODEBANC", T = "ABC"
输出: "BANC"
```
**说明：**

如果 S 中不存这样的子串，则返回空字符串 ""。
如果 S 中存在这样的子串，我们保证它是唯一的答案。



# 题解

## 官方题解
### 1.滑动窗口
**思路：**
在滑动窗口类型的问题中都会有两个指针。一个用于延伸现有窗口的 rightright指针，和一个用于收缩窗口的leftleft 指针。在任意时刻，只有一个指针运动，而另一个保持静止。

![](https://pic.leetcode-cn.com/5171b6699007904e71719eca2a0dcbc5f80cf8242a96c2c86f98ea906a07fc60-image.png)

```
class Solution {
  public String minWindow(String s, String t) {

      if (s.length() == 0 || t.length() == 0) {
          return "";
      }

      // Dictionary which keeps a count of all the unique characters in t.
      Map<Character, Integer> dictT = new HashMap<Character, Integer>();
      for (int i = 0; i < t.length(); i++) {
          int count = dictT.getOrDefault(t.charAt(i), 0);
          dictT.put(t.charAt(i), count + 1);
      }

      // Number of unique characters in t, which need to be present in the desired window.
      int required = dictT.size();

      // Left and Right pointer
      int l = 0, r = 0;

      // formed is used to keep track of how many unique characters in t
      // are present in the current window in its desired frequency.
      // e.g. if t is "AABC" then the window must have two A's, one B and one C.
      // Thus formed would be = 3 when all these conditions are met.
      int formed = 0;

      // Dictionary which keeps a count of all the unique characters in the current window.
      Map<Character, Integer> windowCounts = new HashMap<Character, Integer>();

      // ans list of the form (window length, left, right)
      int[] ans = {-1, 0, 0};

      while (r < s.length()) {
          // Add one character from the right to the window
          char c = s.charAt(r);
          int count = windowCounts.getOrDefault(c, 0);
          windowCounts.put(c, count + 1);

          // If the frequency of the current character added equals to the
          // desired count in t then increment the formed count by 1.
          if (dictT.containsKey(c) && windowCounts.get(c).intValue() == dictT.get(c).intValue()) {
              formed++;
          }

          // Try and co***act the window till the point where it ceases to be 'desirable'.
          while (l <= r && formed == required) {
              c = s.charAt(l);
              // Save the smallest window until now.
              if (ans[0] == -1 || r - l + 1 < ans[0]) {
                  ans[0] = r - l + 1;
                  ans[1] = l;
                  ans[2] = r;
              }

              // The character at the position pointed by the
              // `Left` pointer is no longer a part of the window.
              windowCounts.put(c, windowCounts.get(c) - 1);
              if (dictT.containsKey(c) && windowCounts.get(c).intValue() < dictT.get(c).intValue()) {
                  formed--;
              }

              // Move the left pointer ahead, this would help to look for a new window.
              l++;
          }

          // Keep expanding the window once we are done co***acting.
          r++;
      }

      return ans[0] == -1 ? "" : s.substring(ans[1], ans[2] + 1);
  }
}

```
**复杂度分析：**
- 时间复杂度： O(|S| + |T|)，其中 |S| 和 |T| 代表字符串 S 和 T的长度。在最坏的情况下，可能会对 S 中的每个元素遍历两遍，左指针和右指针各一遍。
- 空间复杂度：O(∣S∣+∣T∣)。当窗口大小等于|S|时为 S。当 |T| 包括全部唯一字符时为 T 。

### 2.优化滑动窗口
**思路：**
我们建立一个 filtered_S列表，其中包括 S 中的全部字符以及它们在S的下标，但这些字符必须在 T中出现。

```
S = "ABCDDDDDDEEAFFBC" T = "ABC"
filtered_S = [(0, 'A'), (1, 'B'), (2, 'C'), (11, 'A'), (14, 'B'), (15, 'C')]
```

此处的(0, 'A')表示字符'A' 在字符串S的下表为0。

现在我们可以在更短的字符串filtered_S中使用滑动窗口法。

```
import javafx.util.Pair;

class Solution {
    public String minWindow(String s, String t) {

        if (s.length() == 0 || t.length() == 0) {
            return "";
        }

        Map<Character, Integer> dictT = new HashMap<Character, Integer>();

        for (int i = 0; i < t.length(); i++) {
            int count = dictT.getOrDefault(t.charAt(i), 0);
            dictT.put(t.charAt(i), count + 1);
        }

        int required = dictT.size();

        // Filter all the characters from s into a new list along with their index.
        // The filtering criteria is that the character should be present in t.
        List<Pair<Integer, Character>> filteredS = new ArrayList<Pair<Integer, Character>>();
        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            if (dictT.containsKey(c)) {
                filteredS.add(new Pair<Integer, Character>(i, c));
            }
        }

        int l = 0, r = 0, formed = 0;
        Map<Character, Integer> windowCounts = new HashMap<Character, Integer>();
        int[] ans = {-1, 0, 0};

        // Look for the characters only in the filtered list instead of entire s.
        // This helps to reduce our search.
        // Hence, we follow the sliding window approach on as small list.
        while (r < filteredS.size()) {
            char c = filteredS.get(r).getValue();
            int count = windowCounts.getOrDefault(c, 0);
            windowCounts.put(c, count + 1);

            if (dictT.containsKey(c) && windowCounts.get(c).intValue() == dictT.get(c).intValue()) {
                formed++;
            }

            // Try and co***act the window till the point where it ceases to be 'desirable'.
            while (l <= r && formed == required) {
                c = filteredS.get(l).getValue();

                // Save the smallest window until now.
                int end = filteredS.get(r).getKey();
                int start = filteredS.get(l).getKey();
                if (ans[0] == -1 || end - start + 1 < ans[0]) {
                    ans[0] = end - start + 1;
                    ans[1] = start;
                    ans[2] = end;
                }

                windowCounts.put(c, windowCounts.get(c) - 1);
                if (dictT.containsKey(c) && windowCounts.get(c).intValue() < dictT.get(c).intValue()) {
                    formed--;
                }
                l++;
            }
            r++;
        }
        return ans[0] == -1 ? "" : s.substring(ans[1], ans[2] + 1);
    }
}


```
**复杂度分析：**
- 时间复杂度： O(∣S∣+∣T∣)， 其中 |S| 和 |T| 分别代表字符串SS 和 TT的长度。 本方法时间复杂度与方法一相同，但当∣filtered_S∣<<<|S|时，复杂度会下降，因为此时迭代次数是 2∗∣filtered_S∣+∣S∣+∣T∣。
- 空间复杂度：O(∣S∣+∣T∣)。



## 其他题解
### 1.滑动窗口
**思路：**
```
class Solution {
    public String minWindow(String s, String t) {
        //把字符串转换为字符数组
        char[] sChars = s.toCharArray();
        char[] pChars = t.toCharArray();

        //
        int[] pMap = new int[128];

        //左指针，右指针
        int i = 0, j = 0; // 考察窗口[i,j-1]

        //还没有覆盖的字符数量
        int count = pChars.length;

        //初始化记录答案的变量
        int minLen = s.length() + 1,l = 0,r = 0;

        //记录t串中每种字符出现的次数
        for (char pChar : pChars)
            pMap[pChar]++;

        while (j < sChars.length) {

            //减小计数
            if (pMap[sChars[j]] > 0)
                count--;
            pMap[sChars[j]]--;
            j++;

            //计数为 0说明区间[i,j-1] 包含 p
            while (count == 0) {

                //更新答案
                if (j - i < minLen) {
                    minLen = j - i;
                    l = i;
                    r = j;
                }

                pMap[sChars[i]]++;
                // 增加计数
                if (pMap[sChars[i]] > 0)
                    count++;
                i++;
            }
        }
        return minLen == s.length() + 1 ? "" : s.substring(l, r);
    }
}
```


---
***参考：
[LeetCode](https://leetcode-cn.com/problems/minimum-window-substring/solution/zui-xiao-fu-gai-zi-chuan-by-leetcode-2/)***
