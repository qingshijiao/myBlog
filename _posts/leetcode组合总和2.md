---
title: 40. 组合总和2（Combination Sum II）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给定一个数组 candidates 和一个目标数 target ，找出 candidates 中所有可以使数字和为 target 的组合。

candidates 中的每个数字在每个组合中只能使用一次。

**说明：**

- 所有数字（包括目标数）都是正整数。
- 解集不能包含重复的组合。 
示例 1:
```
输入: candidates = [10,1,2,7,6,1,5], target = 8,
所求解集为:
[
  [1, 7],
  [1, 2, 5],
  [2, 6],
  [1, 1, 6]
]
```
示例 2:
```
输入: candidates = [2,5,2,1,2], target = 5,
所求解集为:
[
  [1,2,2],
  [5]
]
```




# 题解

## 官方题解
暂无

## 其他题解
### 1.回溯算法
**思路：** 这个和 39 题差不多，都是使用回溯算法 + 栈，不同的是 这一题给定的集合中有重复元素且我们的解集合中不能出现重复元素。这里只要限定条件就可以了。

```
class Solution {
    private void findCombinationSum2(int[] candidates, int begin, int len, int residue, Stack<Integer> stack, List<List<Integer>> res) {
        if (residue == 0) {
            res.add(new ArrayList<>(stack));
            return;
        }
        for (int i = begin; i < len; i++) {
            // 为了避免将负数传递到下一个分支，这里剪枝
            if (residue - candidates[i] < 0) {
                break;
            }

            // 相同部分剪枝
            if (i > begin && candidates[i] == candidates[i - 1]) {
                continue;
            }

            stack.add(candidates[i]);
            findCombinationSum2(candidates, i + 1, len, residue - candidates[i], stack, res);
            stack.pop();
        }
    }

    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        int len = candidates.length;
        List<List<Integer>> res = new ArrayList<>();
        if (len == 0) {
            return res;
        }
        // 先将数组排序，这一步很关键
        Arrays.sort(candidates);
        findCombinationSum2(candidates, 0, len, target, new Stack<>(), res);
        return res;
    }
}
```


---
***参考：
[LeetCode](https://leetcode-cn.com/problems/combination-sum-ii/submissions/)
[liweiwei1419](//leetcode-cn.com/problems/combination-sum-ii/solution/hui-su-suan-fa-jian-zhi-python-dai-ma-java-dai-m-3/)***
