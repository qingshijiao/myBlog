---
title: 3.无重复字符的最长字串Longest Substring Without Repeating Characters)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---

# 题目
给定一个字符串，请你找出其中不含有重复字符的 最长子串 的长度。

示例 1:
>输入: "abcabcbb"
>输出: 3
>解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。

示例 2:
>输入: "bbbbb"
>输出: 1
>解释: 因为无重复字符的最长子串是 "b"，所以其长度为 1。

示例 3:
>输入: "pwwkew"
>输出: 3
>解释: 因为无重复字符的最长子串是 "wke"，所以其长度为 3。
>     请注意，你的答案必须是 子串 的长度，"pwke" 是一个子序列，不是子串。


# 题解

## 官方题解
### 1.暴力法（时间超出）
**思想**：利用两层for循环，逐个检查字符串（PS:可以直接在字符串上进行操作，不必将其转化为字符数组）
```
   public int lengthOfLongestSubstring(String s) {
       int n = s.length();
       int ans = 0;
       for (int i = 0; i < n; i++)
           for (int j = i + 1; j <= n; j++)
               //存入最长字符串个数
               if (allUnique(s, i, j)) ans = Math.max(ans, j - i);
       return ans;
   }

   //利用set特性查看是否有重复字符
   public boolean allUnique(String s, int start, int end) {
       Set<Character> set = new HashSet<>();
       for (int i = start; i < end; i++) {
           Character ch = s.charAt(i);
           if (set.contains(ch)) return false;
           set.add(ch);
       }
       return true;
   }
```

> 复杂度分析
>
> - 时间复杂度：O(n^3)
> - 空间复杂度：O(min(n,m))


### 2.滑动窗口
**思想：** 从暴力法我们可以看出，有很多字符串是重复查找的（比如abc和abca，前面abc我们已经查过没有重复了，但是我们又添加查了一遍）。
通过使用 HashSet 作为滑动窗口，我们可以用 O(1)O(1) 的时间来完成对字符是否在当前的子字符串中的检查。

> **滑动窗口**是数组/字符串问题中常用的抽象概念。 窗口通常是在数组/字符串中由开始和结束索引定义的一系列 元素的集合，即[i, j)（左闭，右开）。而滑动窗口是可以将两个边界向某一方向“滑动”的窗口。例如，我们将 [i, j) 向右滑动 1 个元素，则它将变为 [i+1, j+1)（左闭，右开）。

滑动窗口每次窗口向右移动一格，查找添加的字符是否在前一个窗口内（比如窗口abc和窗口abca，只需证明a是否重复即可，窗口里面的字符均添加在set集合里）。如果字符没有重复，则将字符添加在set（窗口）内；如果重复，则将窗口左边框向右移动(变成bca)。

> **问：** 如果字符串是bcaa，a重复但是删除了b，会不会影响最后结果
> **答：** 并不会，程序中有记录最长长度ans，当窗口为bca时，它的长度已经被记录，删除不影响。
> 由于是重复a，删除时i++，而j还是指第二个a，再次循环仍重复，删除c。这样最后依次删除b，c，a后，添加第二个a就不会出现重复字符了，最长长度ans记录的为3.

```
public int lengthOfLongestSubstring(String s) {
    int n = s.length();
    Set<Character> set = new HashSet<>();
    int ans = 0, i = 0, j = 0;
    while (i < n && j < n) {
        // try to extend the range [i, j]
        if (!set.contains(s.charAt(j))){
            set.add(s.charAt(j++));
            //保留最长字符串
            ans = Math.max(ans, j - i);
        }
        else {
            set.remove(s.charAt(i++));
        }
    }
    return ans;
}
```
> 复杂度分析
>
> - 时间复杂度：O(2n)=O(n)
> - 空间复杂度：O(min(m,n))

### 3.优化滑动窗口
**思想：** 上述的方法最多需要执行 2n 个步骤。事实上，它可以被进一步优化为仅需要 n 个步骤。我们可以定义字符到索引的映射，而不是使用集合来判断一个字符是否存在。 当我们找到重复的字符时，我们可以立即跳过该窗口。
也就是说，如果 s[j] 在 [i, j) 范围内有与 j'重复的字符，我们不需要逐渐增加 i 。 我们可以直接跳过 [i，j']范围内的所有元素，并将 i 变为 j' + 1。
```
//使用HashMap
public class Solution {
    public int lengthOfLongestSubstring(String s) {
        int n = s.length(), ans = 0;
        Map<Character, Integer> map = new HashMap<>(); // current index of character
        // try to extend the range [i, j]
        for (int j = 0, i = 0; j < n; j++) {
            if (map.containsKey(s.charAt(j))) {
                i = Math.max(map.get(s.charAt(j)), i);
            }
            ans = Math.max(ans, j - i + 1);
            //使用j + 1可以检索到重复字符的后一个位置
            map.put(s.charAt(j), j + 1);
        }
        return ans;
    }
}
```
```
//使用ASCII码
public class Solution {
    public int lengthOfLongestSubstring(String s) {
        int n = s.length(), ans = 0;
        int[] index = new int[128]; // current index of character
        // try to extend the range [i, j]
        for (int j = 0, i = 0; j < n; j++) {
            //未出现重复时i=0,出现重复时i=s.charAt(j)重复字符的位置
            i = Math.max(index[s.charAt(j)], i);
            ans = Math.max(ans, j - i + 1);
            index[s.charAt(j)] = j + 1;
        }
        return ans;
    }
}
```
> 复杂度分析
>
> - 时间复杂度：O(n)
> - 空间复杂度（HashMap）：O(min(n, m))
> - 空间复杂度（Table）：O(m), m是字符集大小

## 其他题解
暂时并没有

---
***参考：[领扣](https://leetcode-cn.com/problems/longest-substring-without-repeating-characters/solution/wu-zhong-fu-zi-fu-de-zui-chang-zi-chuan-by-leetcod/)***
