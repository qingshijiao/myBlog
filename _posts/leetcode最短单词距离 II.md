---
title: 244.单词最短距离 II（Shortest Word Distance II）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---

请设计一个类，使该类的构造函数能够接收一个单词列表。然后再实现一个方法，该方法能够分别接收两个单词 word1 和 word2，并返回列表中这两个单词之间的最短距离。您的方法将被以不同的参数调用多次。

示例:
```
假设 words = ["practice", "makes", "perfect", "coding", "makes"]

输入: word1 = “coding”, word2 = “practice”
输出: 3
输入: word1 = "makes", word2 = "coding"
输出: 1
```

注意:
你可以假设 word1 不等于 word2, 并且 word1 和 word2 都在列表里。


#### Solution - 哈希表
因为会多次调用，我们不能每次调用的时候再把这两个单词的下标找出来。我们可以用一个哈希表，在传入字符串数组时，就把每个单词的下标找出存入表中。这样当调用最短距离的方法时，我们只要遍历两个单词的下标列表就行了。具体的比较方法，则类似merge two list，每次比较两个list最小的两个值，得到一个差值。然后把较小的那个给去掉。因为我们遍历输入数组时是从前往后的，所以下标列表也是有序的。

Language: **Java**

```java
public class WordDistance {

    HashMap<String, List<Integer>> map = new HashMap<String, List<Integer>>();

    public WordDistance(String[] words) {
        // 统计每个单词出现的下标存入哈希表中
        for(int i = 0; i < words.length; i++){
            List<Integer> cnt = map.get(words[i]);
            if(cnt == null){
                cnt = new ArrayList<Integer>();
            }
            cnt.add(i);
            map.put(words[i], cnt);
        }
    }

    public int shortest(String word1, String word2) {
        List<Integer> idx1 = map.get(word1);
        List<Integer> idx2 = map.get(word2);
        int distance = Integer.MAX_VALUE;
        int i = 0, j = 0;
        // 每次比较两个下标列表最小的下标，然后把跳过较小的那个
        while(i < idx1.size() && j < idx2.size()){
            distance = Math.min(Math.abs(idx1.get(i) - idx2.get(j)), distance);
            if(idx1.get(i) < idx2.get(j)){
                i++;
            } else {
                j++;
            }
        }
        return distance;
    }
}
```


---
***参考：
[LeetCode](https://leetcode-cn.com/problems/shortest-word-distance-ii/)
[ethannnli](https://segmentfault.com/a/1190000003906667)***
