---
title: 421.数组中两个数的最大异或值 (Maximum XOR of Two Numbers in an Array)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [421\. 数组中两个数的最大异或值](https://leetcode-cn.com/problems/maximum-xor-of-two-numbers-in-an-array/)

Difficulty: **中等**


给定一个非空数组，数组中元素为 a<sub style="display: inline;">0</sub>, a<sub style="display: inline;">1</sub>, a<sub style="display: inline;">2</sub>, … , a<sub style="display: inline;">n-1</sub>，其中 0 ≤ a<sub style="display: inline;">i</sub> < 2<sup>31 </sup>。

找到 a<sub style="display: inline;">i</sub> 和a<sub style="display: inline;">j </sub>最大的异或 (XOR) 运算结果，其中0 ≤ _i_,  _j_ < _n _。

你能在O(_n_)的时间解决这个问题吗？

**示例:**

```
输入: [3, 10, 5, 25, 2, 8]

输出: 28

解释: 最大的结果是 5 ^ 25 = 28.
```


#### Solution

Language: **Java**

```java
​class Solution {
      
    public int findMaximumXOR(int[] nums) {
        int[] l1 = new int[nums.length];
        int[] l0 = new int[nums.length];
        int ind = 31,size1=0,size0=0;
        while (ind>=0 && (size1==0 || size0==0)) {
            size1=0;
            size0=0;
            for (int num : nums) {
                if (((num>>ind)&1)==0) {
                    l0[size0++]=num;
                } else {
                    l1[size1++]=num;
                }
            }
            ind--;
        }
        
        if (size1>0 && size0>0) {
            return dc(l1, size1, l0, size0, ind);
        } else {
            return 0;
        }
    }

    public int dc(int[] l1, int size1, int[] l2, int size2, int ind) {
        if (size1==0 || size2==0) {
            return 0;
        }
        if (ind<0 ||(size1==1 && size2==1)) {
            return l1[0] ^ l2[0];
        }
        int size11=0,size10=0,size21=0,size20=0;
        int[] l11 = new int[size1];
        int[] l10 = new int[size1];
        int[] l21 = new int[size2];
        int[] l20 = new int[size2];
        //System.out.println(size1+","+size2);
        for (int i=0;i<size1;i++) {
            int n=l1[i];
            if (((n>>ind) & 1) == 0) {
                l10[size10++]=n;
            } else {
                l11[size11++]=n;
            }
        }
        for (int i=0;i<size2;i++) {
            int n=l2[i];
            if (((n>>ind) & 1) == 0) {
                l20[size20++]=n;
            } else {
                l21[size21++]=n;
            }
        }
        if ((size10>0 && size11>0) || (size20>0 && size21>0)) {
            return Math.max(dc(l10, size10, l21, size21, ind-1), dc(l11, size11, l20, size20, ind-1));
        } else {
            return dc(l1, size1, l2, size2, ind-1);
        }
        
    }
}
```
---
***参考:
[leetcode](https://leetcode-cn.com/problems/maximum-xor-of-two-numbers-in-an-array/submissions/)***
