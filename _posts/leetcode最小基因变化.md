---
title: 433. 最小基因变化（Minimum Genetic Mutation）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [433\. 最小基因变化](https://leetcode-cn.com/problems/minimum-genetic-mutation/)

Difficulty: **中等**


一条基因序列由一个带有8个字符的字符串表示，其中每个字符都属于 `"A"`, `"C"`, `"G"`, `"T"`中的任意一个。

假设我们要调查一个基因序列的变化。**一次**基因变化意味着这个基因序列中的**一个**字符发生了变化。

例如，基因序列由`"AACCGGTT"` 变化至 `"AACCGGTA" `即发生了一次基因变化。

与此同时，每一次基因变化的结果，都需要是一个合法的基因串，即该结果属于一个基因库。

现在给定3个参数 — start, end, bank，分别代表起始基因序列，目标基因序列及基因库，请找出能够使起始基因序列变化为目标基因序列所需的最少变化次数。如果无法实现目标变化，请返回 -1。

**注意:**

1.  起始基因序列默认是合法的，但是它并不一定会出现在基因库中。
2.  所有的目标基因序列必须是合法的。
3.  假定起始基因序列与目标基因序列是不一样的。

**示例 1:**

```
start: "AACCGGTT"
end:   "AACCGGTA"
bank: ["AACCGGTA"]

返回值: 1
```

**示例 2:**

```
start: "AACCGGTT"
end:   "AAACGGTA"
bank: ["AACCGGTA", "AACCGCTA", "AAACGGTA"]

返回值: 2
```

**示例 3:**

```
start: "AAAAACCC"
end:   "AACCCCCC"
bank: ["AAAACCCC", "AAACCCCC", "AACCCCCC"]

返回值: 3
```


#### Solution

Language: **Java**

```Java
​class Solution {

    private String start;
    private String end;
    private String[] bank;

    private int minStep = Integer.MAX_VALUE;

    public int minMutation(String start, String end, String[] bank) {
        this.start = start;
        this.end = end;
        this.bank = bank;

        helper(new HashSet<String>(), start, 0);
        return minStep == Integer.MAX_VALUE ? -1 : minStep;
    }

    public void helper(HashSet<String> set, String curr, int step) {
        if (curr.equals(end)) {
            minStep = Math.min(minStep, step);
            return;
        }

        for (String compareStr : bank) {
            int diffrent = 0;
            for (int i = 0; i < end.length(); i++) {
                if (compareStr.charAt(i) != curr.charAt(i)) {
                    if (++diffrent > 1)
                        break;
                }
            }

            if (diffrent == 1 && !set.contains(compareStr)) {
                set.add(compareStr);
                helper(set, compareStr, step + 1);
                set.remove(compareStr);
            }
        }

    }

}
```

---
***参考：
[leetcode](https://leetcode-cn.com/problems/minimum-genetic-mutation/submissions/)***
