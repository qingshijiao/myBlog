---
title: 364.加权嵌套序列和 II (Max Sum of Rectangle No Larger Than K)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
题目
给一个嵌套整数序列，请你返回每个数字在序列中的加权和，它们的权重由它们的深度决定。

序列中的每一个元素要么是一个整数，要么是一个序列（这个序列中的每个元素也同样是整数或序列）。

与 前一个问题 不同的是，前一题的权重按照从根到叶逐一增加，而本题的权重从叶到根逐一增加。

也就是说，在本题中，叶子的权重为1，而根拥有最大的权重。

示例 1:
```
输入: [[1,1],2,[1,1]]
输出: 8
解释: 四个 1 在深度为 1 的位置， 一个 2 在深度为 2 的位置。
```
示例 2:
```
输入: [1,[4,[6]]]
输出: 17
解释: 一个 1 在深度为 3 的位置， 一个 4 在深度为 2 的位置，一个 6 在深度为 1 的位置。 13 + 42 + 6*1 = 17。
```

#### Solution

Language: **Java**

```java
​class Solution {
    private int maxDepth=0;

    public int depthSumInverse(List<NestedInteger> nestedList) {
        updateMaxDepth(nestedList,1);
        return getDepthSum(nestedList,1);
    }

    private void updateMaxDepth(List<NestedInteger> nestedList,int depth){
        for(NestedInteger nestedInteger:nestedList){
            if(nestedInteger.isInteger()){
                maxDepth=depth>maxDepth?depth:maxDepth;
            }
            else {
                updateMaxDepth(nestedInteger.getList(),depth+1);
            }
        }
    }

    private int getDepthSum(List<NestedInteger> nestedList,int depth){
        int sum=0;
        for(NestedInteger nestedInteger:nestedList){
            if(nestedInteger.isInteger()){
                sum+=(maxDepth-depth+1) * nestedInteger.getInteger();
            }
            else{
                sum+=getDepthSum(nestedInteger.getList(),depth+1);
            }
        }
        return sum;
    }
}
```
---
***参考:
[coding-gaga](https://www.cnblogs.com/coding-gaga/p/12306019.html)***
