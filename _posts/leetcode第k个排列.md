---
title: 60. 第k个排列（Permutation Sequence）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给出集合 [1,2,3,…,n]，其所有元素共有 n! 种排列。

按大小顺序列出所有排列情况，并一一标记，当 n = 3 时, 所有排列如下：
```
"123"
"132"
"213"
"231"
"312"
"321"
```
给定 n 和 k，返回第 k 个排列。

**说明：**

给定 n 的范围是 [1, 9]。
给定 k 的范围是[1,  n!]。
示例 1:
```
输入: n = 3, k = 3
输出: "213"
```
示例 2:
```
输入: n = 4, k = 9
输出: "2314"
```



# 题解

## 官方题解
暂无

## 其他题解
### 1.剪枝
**思路：**
```
class Solution {
     public String getPermutation(int n, int k) {
        int[] nums = new int[n];
        boolean[] used = new boolean[n];
        for (int i = 0; i < n; i++) {
            nums[i] = i + 1;
            used[i] = false;
        }
        List<String> pre = new ArrayList<>();
        return dfs(nums, used, n, k, 0, pre);
    }

    private int factorial(int n) {
        // 这种编码方式包括了 0 的阶乘是 1 这种情况
        int res = 1;
        while (n > 0) {
            res *= n;
            n -= 1;
        }
        return res;
    }

    private String dfs(int[] nums, boolean[] used, int n, int k, int depth, List<String> pre) {
        if (depth == n) {
            StringBuilder sb = new StringBuilder();
            for (String c : pre) {
                sb.append(c);
            }
            return sb.toString();
        }
        int ps = factorial(n - 1 - depth);
        for (int i = 0; i < n; i++) {
            if (used[i]) {
                continue;
            }
            if (ps < k) {
                k -= ps;
                continue;
            }
            pre.add(nums[i] + "");
            used[i] = true;
            return dfs(nums, used, n, k, depth + 1, pre);
        }
        // 如果参数正确的话，代码不会走到这里
        throw new RuntimeException("参数错误");
    }
}
```
**复杂度分析：**
- 时间复杂度：O(2^N)，回溯算法的时间复杂度是指数级别的，因为我们使用了大量的剪枝操作，故对于解这道问题是可以接受的。
- 空间复杂度：O(N)，nums、used、pre 都与 N 等长，factorial 数组就 10 个数，是常数级别的。


### 2.遍历
**思路：**
```
class Solution {
    public String getPermutation(int n, int k) {
        StringBuilder sb = new StringBuilder();
        //阶乘数组
        int[] factorials = new int[n];
        //注意0和1的阶乘为1
        factorials[0] = 1;
        //阶乘值为当前值乘前一个阶乘值
        for(int i = 1; i < n;i++){
            factorials[i] = i * factorials[i-1];
        }
        //list存储“数字”，因此remove后依旧有序，无需排序。
        //这保证了我们只要知道需要获取值的偏移量就可以得到对应的值。
        List<Character> nums = new ArrayList<>();
        for(int i = 1; i <= n;i++){
            nums.add((char)(i+48));
        }
        int index;
        //将题目的人类习惯奇数改为list内部下标计数。
        k--;
        //最差情况下从第一位一直运算到第n-1位，最后一位便是剩下的。
        for(int j = 1;j < n;j++){
            int factorial = factorials[n-j];
            //获取该位“数字”在list内的下标
            index = k / factorial;
            k = k % factorial;
            //将这一位“数字”加进来后从list内部删除该“数字”
            sb.append(nums.get(index));
            nums.remove(index);
            //如果此时不再有相对偏移量，退出循环。
            if(k == 0){
                break;
            }
        }
        //如果最差情况，此时将最后一位加进来，
        //如果中途因为刚好匹配、没有偏移量而退出则按序将剩余“数字”加进来。
        while (nums.size()>0){
            sb.append(nums.get(0));
            nums.remove(0);
        }
        return sb.toString();
    }
}
```
**复杂度分析：**
- 时间复杂度：O(n^2) 遍历一次处理n位过程中，操作list删除指定位置需要O(n)，因此总时间复杂度为O(n^2)。
- 空间复杂度：O(n) 使用三个O(n)空间分别存储结果、阶乘、数字

### 3.摩拓展开
[摩拓展开](https://blog.csdn.net/modiziri/article/details/22389303)

```
class Solution {
    public String getPermutation(int n, int k) {
        k --;
        ArrayList<Integer> list = new ArrayList<>();
        StringBuilder res = new StringBuilder();
        for(int i = 1; i <= n; i ++) {
            list.add(i);
        }
        int factorial = 1;
        for(int i = 2; i < n; i ++) {
            factorial *= i;
        }
        int factor = n - 1;
        while(factor >= 0) {
            int index = k / factorial;
            res.append(list.get(index));
            list.remove(index);
            k %= factorial;
            if(factor > 0) {
                factorial /= factor;
            }
            factor --;
        }
        return res.toString();
    }
}
```


---
***参考：
[LeetCode](https://leetcode-cn.com/problems/permutation-sequence/submissions/)
[liweiwei1419](https://leetcode-cn.com/problems/permutation-sequence/solution/hui-su-jian-zhi-python-dai-ma-java-dai-ma-by-liwei/)
[noobhan](https://leetcode-cn.com/problems/permutation-sequence/solution/zhao-gui-lu-shu-xue-ji-suan-fa-by-noobhan/)***
