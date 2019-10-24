---
title: 135.分发糖果（Candy）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
老师想给孩子们分发糖果，有 N 个孩子站成了一条直线，老师会根据每个孩子的表现，预先给他们评分。

你需要按照以下要求，帮助老师给这些孩子分发糖果：

- 每个孩子至少分配到 1 个糖果。
- 相邻的孩子中，评分高的孩子必须获得更多的糖果。

那么这样下来，老师至少需要准备多少颗糖果呢？

示例 1:
```
输入: [1,0,2]
输出: 5
解释: 你可以分别给这三个孩子分发 2、1、2 颗糖果。
```
示例 2:
```
输入: [1,2,2]
输出: 4
解释: 你可以分别给这三个孩子分发 1、2、1 颗糖果。
     第三个孩子只得到 1 颗糖果，这已满足上述两个条件。
```


# 题解

## 官方题解
### 1.暴力法
**思路：** 最简单的方法是使用一个一维的数组 candiescandies 去记录给学生的糖果数。

```
public class Solution {
    public int candy(int[] ratings) {
        int[] candies = new int[ratings.length];
        Arrays.fill(candies, 1);
        boolean flag = true;
        int sum = 0;
        while (flag) {
            flag = false;
            for (int i = 0; i < ratings.length; i++) {
                if (i != ratings.length - 1 && ratings[i] > ratings[i + 1] && candies[i] <= candies[i + 1]) {
                    candies[i] = candies[i + 1] + 1;
                    flag = true;
                }
                if (i > 0 && ratings[i] > ratings[i - 1] && candies[i] <= candies[i - 1]) {
                    candies[i] = candies[i - 1] + 1;
                    flag = true;
                }
            }
        }
        for (int candy : candies) {
            sum += candy;
        }
        return sum;
    }
}
```
**复杂度分析：**
- 时间复杂度：O(n^2)。对于每个元素，我们最多要遍历 n 次。
- 空间复杂度：O(n) 。需要一个长度为 n 的 candies 数组。


### 2.用两个数组
**思路：**
![](https://pic.leetcode-cn.com/8d1eb25bdea9343564a0a925a4b9007e62366795785feb112c4ab9c25bd95e0b-file_1559471526790)


```
public class Solution {
    public int candy(int[] ratings) {
        int sum = 0;
        int[] left2right = new int[ratings.length];
        int[] right2left = new int[ratings.length];
        Arrays.fill(left2right, 1);
        Arrays.fill(right2left, 1);
        for (int i = 1; i < ratings.length; i++) {
            if (ratings[i] > ratings[i - 1]) {
                left2right[i] = left2right[i - 1] + 1;
            }
        }
        for (int i = ratings.length - 2; i >= 0; i--) {
            if (ratings[i] > ratings[i + 1]) {
                right2left[i] = right2left[i + 1] + 1;
            }
        }
        for (int i = 0; i < ratings.length; i++) {
            sum += Math.max(left2right[i], right2left[i]);
        }
        return sum;
    }
}

```
**复杂度分析：**
- 时间复杂度：O(n)。 left2right 和 right2left 会各更新一次。
- 空间复杂度：O(n)。 两个数组 left2right 和 right2left 大小都为 n 。


### 3.用一个数组
**思路：**

```
public class Solution {
    public int candy(int[] ratings) {
        int[] candies = new int[ratings.length];
        Arrays.fill(candies, 1);
        for (int i = 1; i < ratings.length; i++) {
            if (ratings[i] > ratings[i - 1]) {
                candies[i] = candies[i - 1] + 1;
            }
        }
        int sum = candies[ratings.length - 1];
        for (int i = ratings.length - 2; i >= 0; i--) {
            if (ratings[i] > ratings[i + 1]) {
                candies[i] = Math.max(candies[i], candies[i + 1] + 1);
            }
            sum += candies[i];
        }
        return sum;
    }
}


```
**复杂度分析：**
- 时间复杂度：O(n) 。长度为 n 数组 candies 被遍历了 3 次。
- 空间复杂度：O(n)。数组 candies 长度为 n 。

### 4.常数空间一次遍历
**思路：**
![](https://pic.leetcode-cn.com/df2bada8d7abe1d0550ebee880b5bf7b00cb38d553f008a9eb25491ddc356533-image.png)

```
class Solution {
    public int candy(int[] ratings) {

        int pre = 1, res = 1, cnt = 0;

        for (int i = 1; i < ratings.length;i++){
            if (ratings[i] >= ratings[i - 1]){
                if (cnt > 0){
                    res += cnt*(1+cnt)/2;
                    if (cnt >= pre){
                        res += (cnt - pre + 1);
                    }
                    cnt = 0;
                    pre = 1;
                }

                pre = (ratings[i] == ratings[i - 1])? 1 : pre + 1;
                res += pre;

            } else{
                cnt++;
            }

        }

        if (cnt > 0){
            res += cnt*(1+cnt)/2;
            if (cnt >= pre){
                res += cnt - pre + 1;
            }
        }

        return res;


    }
}
```

```
public class Solution {
    public int count(int n) {
        return (n * (n + 1)) / 2;
    }
    public int candy(int[] ratings) {
        if (ratings.length <= 1) {
            return ratings.length;
        }
        int candies = 0;
        int up = 0;
        int down = 0;
        int old_slope = 0;
        for (int i = 1; i < ratings.length; i++) {
            int new_slope = (ratings[i] > ratings[i - 1]) ? 1 : (ratings[i] < ratings[i - 1] ? -1 : 0);
            if ((old_slope > 0 && new_slope == 0) || (old_slope < 0 && new_slope >= 0)) {
                candies += count(up) + count(down) + Math.max(up, down);
                up = 0;
                down = 0;
            }
            if (new_slope > 0)
                up++;
            if (new_slope < 0)
                down++;
            if (new_slope == 0)
                candies++;

            old_slope = new_slope;
        }
        candies += count(up) + count(down) + Math.max(up, down) + 1;
        return candies;
    }
}

```
**复杂度分析：**
- 时间复杂度：O(n) 。我们遍历 ratingsratings 数组一次。
- 空间复杂度：O(1) 。使用了常数个变量的额外空间。



## 其他题解
暂无

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/candy/solution/fen-fa-tang-guo-by-leetcode/)***
