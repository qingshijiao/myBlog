---
title: 42. 接雨水（Trapping Rain Water）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给定 n 个非负整数表示每个宽度为 1 的柱子的高度图，计算按此排列的柱子，下雨之后能接多少雨水。
![](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/10/22/rainwatertrap.png)


上面是由数组 [0,1,0,2,1,0,1,3,2,1,2,1] 表示的高度图，在这种情况下，可以接 6 个单位的雨水（蓝色部分表示雨水）。 感谢 Marcos 贡献此图。

示例:
```
输入: [0,1,0,2,1,0,1,3,2,1,2,1]
输出: 6
```



# 题解

## 官方题解
### 1.暴力法
**思路：** 对于每一竖行，找到其左右两边最大的柱子，代表该竖行所能容纳的最大容量，然后再减去改行柱子所占的高度就是储水量。
![](https://i.loli.net/2019/09/14/YbDhk5a3ENRoLVy.png)

```
class Solution {
    public int trap(int[] height) {
        int ans = 0;
        int len = height.length;
        for (int i = 1; i < len - 1; i++) {
            int maxLeft = 0, maxRight = 0;
            for (int j = i; j >= 0; j--) {
                maxLeft = Math.max(maxLeft, height[j]);
            }
            for (int j = i; j < len; j++) {
                maxRight = Math.max(maxRight, height[j]);
            }
            ans += Math.min(maxLeft, maxRight) - height[i];
        }
        return ans;

    }
}
```
**复杂度分析**
- 时间复杂度： O(N^2)。数组中的每个元素都需要向左向右扫描。
- 空间复杂度： O(1) 由于只使用了常数的空间。

### 2.动态规划
**思路：** 和暴力法思路差不多，只不过用了两个数组来存储每个柱子左边和右边最高高度。
![](https://i.loli.net/2019/09/14/dWKy2GahejEHDLC.png)
![](https://i.loli.net/2019/09/14/F3liS1Q5rvfdONe.png)


```
class Solution {
    public int trap(int[] height) {
        if(height == null) {
            return 0;
        }
        int ans = 0;
        int len = height.length;
        int[] leftMax =  new int[len];
        int[] rightMax =  new int[len];
        leftMax[0] = height[0];
        for (int i = 1; i < len; i++) {
            leftMax[i] = Math.max(height[i], leftMax[i - 1]);
        }
        rightMax[len - 1] = height[len - 1];
        for (int i = len - 2; i >= 0; i--) {
            rightMax[i] = Math.max(height[i], rightMax[i + 1]);
        }
        for (int i = 1; i < len - 1; i++) {
            ans += Math.min(leftMax[i], rightMax[i]) - height[i];
        }
        return ans;
    }
}
```
**复杂度分析**
- 时间复杂度： O(N)。
  - 存储最大高度数组，需要两次遍历，每次 O(n) 。
  - 最终使用存储的数据更新 O(n)。
- 空间复杂度： O(n) 额外空间。
  - 和方法 1 相比使用了额外的 O(n) 空间用来放置 leftMax 和 rightMax 数组。

### 3.栈
**思路：** 我们在遍历数组时维护一个栈。如果当前的条形块小于或等于栈顶的条形块，我们将条形块的索引入栈，意思是当前的条形块被栈中的前一个条形块界定。如果我们发现一个条形块长于栈顶，我们可以确定栈顶的条形块被当前条形块和栈的前一个条形块界定，因此我们可以弹出栈顶元素并且累加答案到 ans 。
分隔矩形方法如下：
![](https://i.loli.net/2019/09/14/GaN21wZiCPsLurc.png)
我们知道只有下凹矩形才能储存雨水，所以遍历时 height[current] > height[st.peek()] 满足时我们才进入循环，每遇到一个下凹形状的我们就计算它们其中的面积。

```
class Solution {
    public int trap(int[] height) {
        int ans = 0, current = 0;
        Stack<Integer> st = new Stack<>();
        while (current < height.length) {
            while (!st.empty() && height[current] > height[st.peek()]) {
                int top = st.peek();
                st.pop();
                if (st.empty()) {
                    break;
                }
                int distance = current - st.peek() - 1;
                int boundedHeight = Math.min(height[current], height[st.peek()]) - height[top];
                ans += distance * boundedHeight;
            }
            st.push(current++);
        }
        return ans;
    }
}
```
**复杂度分析**
- 时间复杂度： O(N)。
  - 单次遍历 O(n)，每个条形块最多访问两次（由于栈的弹入和弹出），并且弹入和弹出栈都是 O(1) 的。
- 空间复杂度： O(n) 额外空间。
  -  栈最多在阶梯型或平坦型条形块结构中占用 O(n) 的空间。



### 4.双指针
**思路：** 划分矩形的方式不同。
![06](https://i.loli.net/2019/09/14/UYITcDRQF4fgSVk.png)
短板效应，短的板向中间移动，从而使储水量上升。
```
class Solution {
    public int trap(int[] height) {
      int left = 0, right = height.length - 1;
      int ans = 0;
      int leftMax = 0, rightMax = 0;
      while (left < right) {
          if (height[left] < height[right]) {
              if (height[left] >= leftMax) {
                  leftMax = height[left];
              } else {
                  ans += (leftMax - height[left]);
              }
              ++left;
          } else {
              if (height[right] >= rightMax) {
                  rightMax = height[right];
              } else {
                  ans += (rightMax - height[right]);
              }
              --right;
          }
      }
      return ans;
    }
}
```
**复杂度分析**
- 时间复杂度： O(N)。
  - 单次遍历的时间O(n)。
- 空间复杂度： O(n) 额外空间。
  - left, right, leftMax 和 rightMax 只需要常数的空间。


## 其他题解
### 1.挖地法
**思路：** 其实是按行进行划分矩阵，不过算法很有趣，就放在这。
![](https://i.loli.net/2019/09/14/Xxp7n5iGtYf6jqA.png)
[0,1,0,2,1,0,1,3,2,1,2,1]
1.先把左右两头的平地挖掉。
[1,0,2,1,0,1,3,2,1,2,1]
2.再按左右两堵墙矮的为基准，把地平面向下挖这个高度。
[0,-1,1,0,-1,0,2,1,0,1,0]
3.负数代表挖出了洞，浇水泥填平，共浇水泥2单位
[0,0,1,0,0,0,2,1,0,1,0]
循环前三步直到地被挖完，记录水泥浇灌量。


### 2.翻山越岭填坑
**思路：** 遍历一次找到最大值，左右两边分别遍历依次补全，即可得雨水收集量。
![](https://i.loli.net/2019/09/14/cGwEYWQJM2nOpAm.png)

```
class Solution {
    public int trap(int[] height) {
        int max = 0;
        int maxIndex = 0;
        //寻找A点
        for (int i = 0; i < height.length; i++) {
            if(height[i]>max){
                max = height[i];
                maxIndex =i;
            }
        }
        int maxLeft = 0;
        int result = 0;
        //计算left-A的雨水收集
        for (int i = 0; i < maxIndex; i++) {
            if(height[i]>maxLeft){
                maxLeft = height[i];
            }else {
                result += maxLeft-height[i];
            }
        }
        int maxRight = 0;
        //计算A-left的雨水收集
        for (int i = height.length-1; i > maxIndex ; i--) {
            if(height[i]>maxRight){
                maxRight = height[i];
            }else {
                result += maxRight - height[i];
            }
        }
        return result;
    }
}
```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/trapping-rain-water/solution/jie-yu-shui-by-leetcode/)
[liweiwei1419](https://leetcode-cn.com/problems/first-missing-positive/solution/tong-pai-xu-python-dai-ma-by-liweiwei1419/)
[huxixx](https://leetcode-cn.com/problems/trapping-rain-water/solution/wa-di-fa-by-huxixx/)
[15002725623](https://leetcode-cn.com/problems/trapping-rain-water/solution/javabian-li-yi-ci-zhao-dao-zui-da-zhi-zuo-you-lian/)***
