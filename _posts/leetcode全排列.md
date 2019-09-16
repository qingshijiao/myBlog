---
title: 46. 全排列（Permutations）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给定一个没有重复数字的序列，返回其所有可能的全排列。

示例:
```
输入: [1,2,3]
输出:
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
```


# 题解

## 官方题解
暂无

## 其他题解
### 1.回溯算法
**思路：**

```
class Solution {
    public List<List<Integer>> permute(int[] nums) {

        List<List<Integer>> res = new ArrayList<>();
        int[] visited = new int[nums.length];
        backtrack(res, nums, new ArrayList<Integer>(), visited);
        return res;

    }

    private void backtrack(List<List<Integer>> res, int[] nums, ArrayList<Integer> tmp, int[] visited) {
        if (tmp.size() == nums.length) {
            res.add(new ArrayList<>(tmp));
            return;
        }
        for (int i = 0; i < nums.length; i++) {
            if (visited[i] == 1) continue;
            visited[i] = 1;
            tmp.add(nums[i]);
            backtrack(res, nums, tmp, visited);
            visited[i] = 0;
            tmp.remove(tmp.size() - 1);
        }
    }

}
```
**复杂度分析**
- 时间复杂度：
- 空间复杂度：


---
***参考：
[powcai](https://leetcode-cn.com/problems/permutations/solution/hui-su-suan-fa-by-powcai-2/)***
