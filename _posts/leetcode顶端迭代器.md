---
title: 284.顶端迭代器 (Peeking Iterator)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [284\. 顶端迭代器](https://leetcode-cn.com/problems/peeking-iterator/)

Difficulty: **中等**


给定一个迭代器类的接口，接口包含两个方法： `next()` 和 `hasNext()`。设计并实现一个支持 `peek()` 操作的顶端迭代器 -- 其本质就是把原本应由 `next()` 方法返回的元素 `peek()` 出来。

**示例:**

```
假设迭代器被初始化为列表 [1,2,3]。

调用 next() 返回 1，得到列表中的第一个元素。
现在调用 peek() 返回 2，下一个元素。在此之后调用 next() 仍然返回 2。
最后一次调用 next() 返回 3，末尾元素。在此之后调用 hasNext() 应该返回 false。
```

**进阶：**你将如何拓展你的设计？使之变得通用化，从而适应所有的类型，而不只是整数型？


#### Solution

Language: **Java**

```java
​// Java Iterator interface reference:
// https://docs.oracle.com/javase/8/docs/api/java/util/Iterator.html
class PeekingIterator implements Iterator<Integer> {
private Iterator<Integer> iterator;
    private Integer cache = null; // 第一次peek时, 缓存迭代的元素

    public PeekingIterator(Iterator<Integer> iter) {
        iterator = iter;
    }

    public Integer peek() {
        if (cache == null)
            cache = iterator.next();
        return cache;
    }

    @Override
    public Integer next() {
        if (cache == null)
            return iterator.next();
        Integer temp = cache;
        cache = null;
        return temp;
    }

    @Override
    public boolean hasNext() {
        return cache != null || iterator.hasNext();
    }
}
```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/peeking-iterator/submissions/)
[xteaj](https://leetcode-cn.com/problems/peeking-iterator/solution/java-yong-yi-ge-bian-liang-ji-lu-peek-zhi-by-xteaj/)***
