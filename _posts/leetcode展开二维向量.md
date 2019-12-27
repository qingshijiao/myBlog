---
title: 251.展开二维向量（Flatten 2D Vector）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
Design and implement an iterator to flatten a 2d vector. It should support the following operations: next and hasNext.

Example:
```
Vector2D iterator = new Vector2D([[1,2],[3],[4]]);

iterator.next(); // return 1
iterator.next(); // return 2
iterator.next(); // return 3
iterator.hasNext(); // return true
iterator.hasNext(); // return true
iterator.next(); // return 4
iterator.hasNext(); // return false
```

**Notes:**

- Please remember to RESET your class variables declared in Vector2D, as static/class variables are persisted across multiple test cases. Please see here for more details.
- You may assume that next() call will always be valid, that is, there will be at least a next element in the 2d vector when next() is called.


**Follow up:**

> As an added challenge, try to code it using only iterators in C++ or iterators in Java.


#### Solution - 链表

Language: **Java**

```java
import java.util.ArrayList;
import java.util.Iterator;
import java.util.List;

public class Vector2D implements Iterator<Integer> {
    private List<Integer> list = new ArrayList<>();

    public Vector2D(List<List<Integer>> vec2d) {
        // Initialize your data structure here
        for (int i = 0; i < vec2d.size(); i++) {
            List<Integer> integers = vec2d.get(i);
            list.addAll(integers);
        }
    }

    private int currentIndex = 0;

    @Override
    public Integer next() {
        // Write your code here
        Integer integer = list.get(currentIndex);
        currentIndex++;
        return integer;
    }

    @Override
    public boolean hasNext() {
        // Write your code here
        return currentIndex < list.size();
    }

    @Override
    public void remove() {
        list.remove(currentIndex);
    }
}

/**
 * Your Vector2D object will be instantiated and called as such:
 * Vector2D i = new Vector2D(vec2d);
 * while (i.hasNext()) v[f()] = i.next();
 */

```
---
***参考：
[代码先锋网](https://www.codeleading.com/article/7589617173/)***
