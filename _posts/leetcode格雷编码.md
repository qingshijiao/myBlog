---
title: 89.格雷编码（Gray Code）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
格雷编码是一个二进制数字系统，在该系统中，两个连续的数值仅有一个位数的差异。

给定一个代表编码总位数的非负整数 n，打印其格雷编码序列。格雷编码序列必须以 0 开头。

示例 1:
```
输入: 2
输出: [0,1,3,2]
解释:
00 - 0
01 - 1
11 - 3
10 - 2

对于给定的 n，其格雷编码序列并不唯一。
例如，[0,2,3,1] 也是一个有效的格雷编码序列。

00 - 0
10 - 2
11 - 3
01 - 1
```
示例 2:
```
输入: 0
输出: [0]
解释: 我们定义格雷编码序列必须以 0 开头。
     给定编码总位数为 n 的格雷编码序列，其长度为 2n。当 n = 0 时，长度为 20 = 1。
     因此，当 n = 0 时，其格雷编码序列为 [0]。
```

# 题解

## 官方题解
暂无


## 其他题解

### 1.镜像反射法
**思路：**

![](https://pic.leetcode-cn.com/d0df7e038c396acf7c5283e8080963ecefe2ab37d4b607982eb3e40b1e5ee03b-Picture3.png)

```
class Solution {
    public List<Integer> grayCode(int n) {
        List<Integer> res = new ArrayList<Integer>() {{ add(0); }};
        int head = 1;
        for (int i = 0; i < n; i++) {
            for (int j = res.size() - 1; j >= 0; j--)
                res.add(head + res.get(j));
            head <<= 1;
        }
        return res;
    }
}
```
**复杂度分析：**
- 时间复杂度：O(2^n)。
- 空间复杂度：O(1)。


### 2.直接推导
**思路：**
以 n = 3 为例。
- 0 0 0 第零项初始化为 0。
- 0 0 1 第一项改变上一项最右边的位元
- 0 1 1 第二项改变上一项右起第一个为 1 的位元的左边位
- 0 1 0 第三项同第一项，改变上一项最右边的位元
- 1 1 0 第四项同第二项，改变最上一项右起第一个为 1 的位元的左边位
- 1 1 1 第五项同第一项，改变上一项最右边的位元
- 1 0 1 第六项同第二项，改变最上一项右起第一个为 1 的位元的左边位
- 1 0 0 第七项同第一项，改变上一项最右边的位元


```
class Solution {
    public List<Integer> grayCode(int n) {
        List<Integer> gray = new ArrayList<Integer>();
        gray.add(0); //初始化第零项
        for (int i = 1; i < 1 << n; i++) {
            //得到上一个的值
            int previous = gray.get(i - 1);
            //同第一项的情况
            if (i % 2 == 1) {
                previous ^= 1; //和 0000001 做异或，使得最右边一位取反
                gray.add(previous);
            //同第二项的情况
            } else {
                int temp = previous;
                //寻找右边起第第一个为 1 的位元
                for (int j = 0; j < n; j++) {
                    if ((temp & 1) == 1) {
                        //和 00001000000 类似这样的数做异或，使得相应位取反
                        previous = previous ^ (1 << (j + 1));
                        gray.add(previous);
                        break;
                    }
                    temp = temp >> 1;
                }
            }
        }
        return gray;
    }

}
```
**复杂度分析：**
- 时间复杂度：O(2^n)。
- 空间复杂度：O(1)。


### 3.公式
**思路：**
![](https://pic.leetcode-cn.com/1013850d7f6c8cf1d99dc0ac3292264b74f6a52d84e0215f540c80952e184f41-image.png)


```
class Solution {
    public List<Integer> grayCode(int n) {
      List<Integer> gray = new ArrayList<Integer>();
      for(int binary = 0;binary < 1 << n; binary++){
          gray.add(binary ^ binary >> 1);
      }
      return gray;
    }

}
```
**复杂度分析：**
- 时间复杂度：O(2^n)。
- 空间复杂度：O(1)。

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/merge-sorted-array/solution/he-bing-liang-ge-you-xu-shu-zu-by-leetcode/)
[windliang](https://leetcode-cn.com/problems/gray-code/solution/xiang-xi-tong-su-de-si-lu-fen-xi-duo-jie-fa-by--12/)***
