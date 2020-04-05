---
title: 341.至多包含 K 个不同字符的最长子串 (Flatten Nested List Iterator)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [341\. 扁平化嵌套列表迭代器](https://leetcode-cn.com/problems/flatten-nested-list-iterator/)

Difficulty: **中等**


给你一个嵌套的整型列表。请你设计一个迭代器，使其能够遍历这个整型列表中的所有整数。

列表中的每一项或者为一个整数，或者是另一个列表。其中列表的元素也可能是整数或是其他列表。

**示例 1:**

```
输入: [[1,1],2,[1,1]]
输出: [1,1,2,1,1]
解释: 通过重复调用 next 直到 hasNext 返回 false，next 返回的元素的顺序应该是: [1,1,2,1,1]。
```

**示例 2:**

```
输入: [1,[4,[6]]]
输出: [1,4,6]
解释: 通过重复调用 next 直到 hasNext 返回 false，next 返回的元素的顺序应该是: [1,4,6]。
```

#### Solution

Language: **Java**

```java
​/**
 * // This is the interface that allows for creating nested lists.
 * // You should not implement it, or speculate about its implementation
 * public interface NestedInteger {
 *
 *     // @return true if this NestedInteger holds a single integer, rather than a nested list.
 *     public boolean isInteger();
 *
 *     // @return the single integer that this NestedInteger holds, if it holds a single integer
 *     // Return null if this NestedInteger holds a nested list
 *     public Integer getInteger();
 *
 *     // @return the nested list that this NestedInteger holds, if it holds a nested list
 *     // Return null if this NestedInteger holds a single integer
 *     public List<NestedInteger> getList();
 * }
 */

public class NestedIterator implements Iterator<Integer> {

    private List<Integer> list;
    private int index;

    public NestedIterator(List<NestedInteger> nestedList) {
        list = new ArrayList<>();
        index = 0;
        splitList(nestedList);
    }
    //递归
    private void splitList(List<NestedInteger> nestedList){
        for(NestedInteger node: nestedList){
            //若当前节点是list，则递归
            if(!node.isInteger()){
                splitList(node.getList());
            }else{
                list.add(node.getInteger());
            }
        }
    }

    @Override
    public Integer next() {
        return list.get(index++);
    }

    @Override
    public boolean hasNext() {
        return index < list.size();
    }
}

/**
 * Your NestedIterator object will be instantiated and called as such:
 * NestedIterator i = new NestedIterator(nestedList);
 * while (i.hasNext()) v[f()] = i.next();
 */
```

---
***参考:
[leetcode](https://leetcode-cn.com/problems/flatten-nested-list-iterator/submissions/)***
