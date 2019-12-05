---
title: 216.组合总和 III（Combination Sum III）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [216\. 组合总和 III](https://leetcode-cn.com/problems/combination-sum-iii/)

Difficulty: **中等**


找出所有相加之和为 _**n**_ 的 **_k _**个数的组合**_。_**组合中只允许含有 1 - 9 的正整数，并且每种组合中不存在重复的数字。

**说明：**

*   所有数字都是正整数。
*   解集不能包含重复的组合。 

**示例 1:**

```
输入: k = 3, n = 7
输出: [[1,2,4]]
```

**示例 2:**

```
输入: k = 3, n = 9
输出: [[1,2,6], [1,3,5], [2,3,4]]
```


#### Solution1 - 回溯 + 剪枝

Language: **Java**

```java
​class Solution {
    List<List<Integer>> res = new ArrayList<>();
    int k=0;
    public List<List<Integer>> combinationSum3(int k, int n) {
        this.k = k;  //省得回溯函数参数列表太长了，所以单独把k提出来
        backstrap(new Stack<Integer>(), 0, 1, n);  //临时栈存放结果数组
        return res;
    }
    private void backstrap(Stack<Integer> tmp, int heigh, int start, int residual){
        if(heigh>k) return;   //高度过高直接剪枝
        if(heigh==k && residual==0){
            res.add(new ArrayList<Integer>(tmp));   //找到匹配结果写入res列表
            return;
        }
        for(int i = start; i<10 && residual-i>=0; i++){  //将数减成负数，不可能继续下去，进行剪枝
            tmp.push(i);
            backstrap(tmp, heigh+1, i+1, residual-i);
            tmp.pop();  //回退栈结果，回溯
        }

    }
}

```


#### Solution2 - DFS

Language: **Java**

```java
class Solution {
    public List<List<Integer>> combinationSum3(int k, int n) {
        List<List<Integer>> result = new ArrayList<>();
        if (k > 9 || k * 9 < n) {
            return result;
        }
        boolean[] mark = new boolean[9];
        depthFirstSearch(0, n, k, mark, result);
        return result;
    }

    private void depthFirstSearch(int curr, int sum, int depth, boolean[] mark, List<List<Integer>> result) {
        if (depth == 0) {
            if (sum == 0) {
                List<Integer> item = new ArrayList<>();
                for (int i = 0, z = mark.length; i < z; i++) {
                    if (mark[i]) {
                        item.add(i + 1);
                    }
                }
                result.add(item);
            }
            return;
        }
        for (int i = curr, z = mark.length; i < z; i++) {
            if (sum - (i + 1) >= 0) {
                mark[i] = true;
                depthFirstSearch(i + 1, sum - (i + 1), depth - 1, mark, result);
                mark[i] = false;
            } else {
                break;
            }
        }
    }
}
```


---
***参考：
[LeetCode](https://leetcode-cn.com/problems/combination-sum-iii/submissions/)
[yecheng](https://leetcode-cn.com/problems/combination-sum-iii/solution/javahui-su-jian-zhi-1ms-by-yecheng/)***
