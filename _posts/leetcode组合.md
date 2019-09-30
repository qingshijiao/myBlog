---
title: 77. 组合（Combinations）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给定两个整数 n 和 k，返回 1 ... n 中所有可能的 k 个数的组合。

示例:
```
输入: n = 4, k = 2
输出:
[
  [2,4],
  [3,4],
  [2,3],
  [1,2],
  [1,3],
  [1,4],
]
```


# 题解

## 官方题解
### 1.回溯算法
**思路：**
类似组合、排列数。回溯法是一种通过遍历所有可能成员来寻找全部可行解的算法。若候选 不是 可行解 (或者至少不是 最后一个 解)，回溯法会在前一步进行一些修改以舍弃该候选，换而言之， 回溯 并再次尝试。

```
class Solution {
  List<List<Integer>> output = new LinkedList();
  int n;
  int k;

  public void backtrack(int first, LinkedList<Integer> curr) {
    // if the combination is done
    if (curr.size() == k)
      output.add(new LinkedList(curr));

    for (int i = first; i < n + 1; ++i) {
      // add i into the current combination
      curr.add(i);
      // use next integers to complete the combination
      backtrack(i + 1, curr);
      // backtrack
      curr.removeLast();
    }
  }

  public List<List<Integer>> combine(int n, int k) {
    this.n = n;
    this.k = k;
    backtrack(1, new LinkedList<Integer>());
    return output;
  }
}

```
![](https://i.loli.net/2019/09/30/UpJdAcnrGKzaPB7.png)


### 2.字典序(二进制排序) 组合
**思路：**
主要思路是以字典序的顺序获得全部组合。
![](https://pic.leetcode-cn.com/ab26203eb768a3153fe704cfee97158429d08e886f7e5b453b2256ee658f0598-image.png)


```
class Solution {
  public List<List<Integer>> combine(int n, int k) {
    // init first combination
    LinkedList<Integer> nums = new LinkedList<Integer>();
    for(int i = 1; i < k + 1; ++i)
      nums.add(i);
    nums.add(n + 1);

    List<List<Integer>> output = new ArrayList<List<Integer>>();
    int j = 0;
    while (j < k) {
      // add current combination
      output.add(new LinkedList(nums.subList(0, k)));
      // increase first nums[j] by one
      // if nums[j] + 1 != nums[j + 1]
      j = 0;
      while ((j < k) && (nums.get(j + 1) == nums.get(j) + 1))
        nums.set(j, j++ + 1);
      nums.set(j, nums.get(j) + 1);
    }
    return output;
  }
}

```
![](https://i.loli.net/2019/09/30/geBQql9p1TKfsPb.png)



## 其他题解
### 1.回溯
**思路：**

```
class Solution {
    public List<List<Integer>> combine(int n, int k) {
        List<List<Integer>> res = new ArrayList<>();
        backtrack(n,1,k,new ArrayList<Integer>(),res);
        return res;
    }

    private void backtrack(int n , int start, int k , List<Integer> tmp_list , List<List<Integer>> res){
        if(k == 0){
            res.add(new ArrayList<Integer>(tmp_list));
            return;
        }
        for(int i = start ; i < n - k + 2 ; i++){
            tmp_list.add(i);
            backtrack(n,i+1,k-1,tmp_list,res);
            tmp_list.remove(tmp_list.size()-1);
        }
    }
}

```


---
***参考：
[LeetCode](https://leetcode-cn.com/problems/combinations/solution/zu-he-by-leetcode/)***
