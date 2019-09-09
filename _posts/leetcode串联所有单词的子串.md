---
title: 30. 串联所有单词的子串（Substring with Concatenation of All Words）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给定一个字符串 s 和一些长度相同的单词 words。找出 s 中恰好可以由 words 中所有单词串联形成的子串的起始位置。

注意子串要与 words 中的单词完全匹配，中间不能有其他字符，但不需要考虑 words 中单词串联的顺序。

 

示例 1：
```
输入：
  s = "barfoothefoobarman",
  words = ["foo","bar"]
输出：[0,9]
解释：
从索引 0 和 9 开始的子串分别是 "barfoor" 和 "foobar" 。
输出的顺序不重要, [9,0] 也是有效答案。
```
示例 2：
```
输入：
  s = "wordgoodgoodgoodbestword",
  words = ["word","good","best","word"]
输出：[]
```


# 题解

## 官方题解
暂无

## 其他题解
### 1.字典
**思路：** 截取字符串 s 中一定长度（words 单词长度和），形成字串，将字串截取相同长度（与 words 单词长度相同）形成 tmp（HashMap），和 words 形成的 map比较。

```
class Solution {
    public List<Integer> findSubstring(String s, String[] words) {
        List<Integer> res = new ArrayList<>();
        if (s == null || s.length() == 0 || words == null || words.length == 0) return res;
        HashMap<String, Integer> map = new HashMap<>();
        int one_word = words[0].length();
        int word_num = words.length;
        int all_len = one_word * word_num;
        for (String word : words) {
            map.put(word, map.getOrDefault(word, 0) + 1);
        }
        for (int i = 0; i < s.length() - all_len + 1; i++) {
            String tmp = s.substring(i, i + all_len);
            HashMap<String, Integer> tmp_map = new HashMap<>();
            for (int j = 0; j < all_len; j += one_word) {
                String w = tmp.substring(j, j + one_word);
                tmp_map.put(w, tmp_map.getOrDefault(w, 0) + 1);
            }
            if (map.equals(tmp_map)) res.add(i);
        }
        return res;
    }
}
```

### 2.滑动窗口
**思路：** 符合的话，right 向后移动一个单词距离，不符合则 left 先后移动一个距离，直到符合。
> for 遍历长度只有 one_word 的原因是成组组合不同
> 比如abcdefghi，三个为一组
> - abc def ghi
> - bcd efg
> - cde fgh
>
> 假设 abc 在 words 中，它符合会与 def 再结合，不符合则舍弃 left 加一个单词长度。这里我们看到，如果 for 的遍历 i 扩大到 3，left = i = 3, 这和舍弃 abc 的情况重复了，所以 for 遍历长度只用 one_word 就可以。
```
class Solution {
    public List<Integer> findSubstring(String s, String[] words) {
        List<Integer> res = new ArrayList<>();
        if (s == null || s.length() == 0 || words == null || words.length == 0) return res;
        HashMap<String, Integer> map = new HashMap<>();
        int one_word = words[0].length();
        int word_num = words.length;
        int all_len = one_word * word_num;
        for (String word : words) {
            map.put(word, map.getOrDefault(word, 0) + 1);
        }
        for (int i = 0; i < one_word; i++) {
            int left = i, right = i, count = 0;
            HashMap<String, Integer> tmp_map = new HashMap<>();
            while (right + one_word <= s.length()) {
                String w = s.substring(right, right + one_word);
                tmp_map.put(w, tmp_map.getOrDefault(w, 0) + 1);
                right += one_word;
                count++;
                while (tmp_map.getOrDefault(w, 0) > map.getOrDefault(w, 0)) {
                    String t_w = s.substring(left, left + one_word);
                    count--;
                    tmp_map.put(t_w, tmp_map.getOrDefault(t_w, 0) - 1);
                    left += one_word;
                }
                if (count == word_num) res.add(left);

            }
        }

        return res;
    }
}
```

### 3.滑动窗口
**思路：** 和 2 相比，这个优化的是如果新添加的单词不在 map 中，那么直接跳过(left = right)，tmp清空，重新开始查找。而 2 中则是left向右移动一个单词距离，直到满足。节省了移动距离的时间。
```
public List<Integer> findSubstring(String s, String[] words) {
    List<Integer> res = new ArrayList<>();
    if (s == null || s.length() == 0 || words == null || words.length == 0) {
        return res;
    }
    HashMap<String, Integer> map = new HashMap<>();
    int one_word = words[0].length();
    int word_num = words.length;
    int all_len = one_word * word_num;
    for (String word : words) {
        map.put(word, map.getOrDefault(word, 0) + 1);
    }
    for (int i = 0; i < one_word; i++) {
        int left = i, right = i, count = 0;
        HashMap<String, Integer> tmp_map = new HashMap<>();
        while (right + one_word <= s.length()) {
            String w = s.substring(right, right + one_word);
            right += one_word;
            if (!map.containsKey(w)) {
                count = 0;
                left = right;
                tmp_map.clear();
            } else {
                tmp_map.put(w, tmp_map.getOrDefault(w, 0) + 1);
                count++;
                while (tmp_map.getOrDefault(w, 0) > map.getOrDefault(w, 0)) {
                    String t_w = s.substring(left, left + one_word);
                    count--;
                    tmp_map.put(t_w, tmp_map.getOrDefault(t_w, 0) - 1);
                    left += one_word;
                }
                if (count == word_num) {
                    res.add(left);
                }
            }
        }
    }
    return res;
}

```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/substring-with-concatenation-of-all-words)
[powcai](https://leetcode-cn.com/problems/substring-with-concatenation-of-all-words/solution/chuan-lian-suo-you-dan-ci-de-zi-chuan-by-powcai/)***
