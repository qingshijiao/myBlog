---
title: 438. 找到字符串中所有字母异位词 (Find All Anagrams in a String)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [438\. 找到字符串中所有字母异位词](https://leetcode-cn.com/problems/find-all-anagrams-in-a-string/)

Difficulty: **中等**


给定一个字符串 **s **和一个非空字符串 **p**，找到 **s **中所有是 **p **的字母异位词的子串，返回这些子串的起始索引。

字符串只包含小写英文字母，并且字符串 **s **和 **p **的长度都不超过 20100。

**说明：**

*   字母异位词指字母相同，但排列不同的字符串。
*   不考虑答案输出的顺序。

**示例 1:**

```
输入:
s: "cbaebabacd" p: "abc"

输出:
[0, 6]

解释:
起始索引等于 0 的子串是 "cba", 它是 "abc" 的字母异位词。
起始索引等于 6 的子串是 "bac", 它是 "abc" 的字母异位词。
```

** 示例 2:**

```
输入:
s: "abab" p: "ab"

输出:
[0, 1, 2]

解释:
起始索引等于 0 的子串是 "ab", 它是 "ab" 的字母异位词。
起始索引等于 1 的子串是 "ba", 它是 "ab" 的字母异位词。
起始索引等于 2 的子串是 "ab", 它是 "ab" 的字母异位词。
```


#### Solution

Language: **Java**

```java
​class Solution {
    public List<Integer> findAnagrams(String s, String p) {
        List<Integer> resultList = new ArrayList<>();
		//1. 参数校验
		if(s.length() < p.length()){
			return resultList;
		}
		//2. 初始化参数
		char[] sArr = s.toCharArray();
		char[] pArr = p.toCharArray();
		int sLen = s.length();
		int pLen = p.length();
		//定义目标字符串的窗口, 由于这里都是小写字母,所以可以这么做 这里也可以用map 来保存窗口 TODO
		int[] needs = new int[26];
		//定义当前窗口
		int[] window = new int[26];

		//3. 初始化目标窗口
		for(int i=0; i<pLen; i++){
			needs[pArr[i]-'a']++;
		}

		//4. 窗口滑动
		int left = 0;
		int right = 0;
		while (right < sLen){
			//移动右边窗口
			int curR = sArr[right] - 'a';
			right++;
			window[curR]++;

			//如果出现一不一致的情况, 则将left 指针和right指针 合并在一起，并清空其中的数据
			while(window[curR] > needs[curR]){
				//移动左指针
				int curL = sArr[left] -'a';
				left++; //最终left 和 right会合并在一起, 所以可以采用这个操作
				window[curL]--;
			}
			if(right - left == pLen){
				resultList.add(left);
			}
		}

		return resultList;
    }
}
```

---
***参考:
[leetcode](https://leetcode-cn.com/problems/find-all-anagrams-in-a-string/submissions/)***
