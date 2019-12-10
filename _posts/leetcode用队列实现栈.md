---
title: 225.用队列实现栈（Implement Stack using Queues）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [225\. 用队列实现栈](https://leetcode-cn.com/problems/implement-stack-using-queues/)

Difficulty: **简单**


使用队列实现栈的下列操作：

*   push(x) -- 元素 x 入栈
*   pop() -- 移除栈顶元素
*   top() -- 获取栈顶元素
*   empty() -- 返回栈是否为空

**注意:**

*   你只能使用队列的基本操作-- 也就是 `push to back`, `peek/pop from front`, `size`, 和 `is empty` 这些操作是合法的。
*   你所使用的语言也许不支持队列。 你可以使用 list 或者 deque（双端队列）来模拟一个队列 , 只要是标准的队列操作即可。
*   你可以假设所有操作都是有效的（例如, 对一个空的栈不会调用 pop 或者 top 操作）。


#### Solution1 - 两个队列，压入 -O(1)， 弹出 -O(n)

![](https://pic.leetcode-cn.com/73b3988402ba76f30372520cd8a3dd77afd4f2bf54020966f4b8975708e84dc9-file_1561370741978)
![](https://pic.leetcode-cn.com/558b9e9258a8ba35c6456ea714d05f55d35da3c3306bef8fa47099093a3ab5b7-file_1561370741978)

Language: **Java**

```java
​private Queue<Integer> q1 = new LinkedList<>();
private Queue<Integer> q2 = new LinkedList<>();
private int top;

// Push element x onto stack.
public void push(int x) {
    q1.add(x);
    top = x;
}

// Removes the element on top of the stack.
public void pop() {
    while (q1.size() > 1) {
        top = q1.remove();
        q2.add(top);
    }
    q1.remove();
    Queue<Integer> temp = q1;
    q1 = q2;
    q2 = temp;
}


```

#### Solution2 - 两个队列，压入 -O(n)， 弹出 -O(1)

![](https://pic.leetcode-cn.com/1acd10c255534e86719cf83b07f294c76967687c52db3ec44367d0cb7c45483e-file_1561370741978)
![](https://pic.leetcode-cn.com/fc27d76b78bbe094f6912a0aa56dee5f8e618a4f04834ab043eb39ecb2e0cc93-file_1561370741978)

Language: **Java**

```java
​public void push(int x) {
    q2.add(x);
    top = x;
    while (!q1.isEmpty()) {
        q2.add(q1.remove());
    }
    Queue<Integer> temp = q1;
    q1 = q2;
    q2 = temp;
}

// Removes the element on top of the stack.
public void pop() {
    q1.remove();
    if (!q1.isEmpty()) {
    	top = q1.peek();
    }
}

// Return whether the stack is empty.
public void empty() {
    ruturn q1.isEmpty();
}


// Get the top element.
public int top() {
    return top;
}

```

#### Solution3 - 一个队列， 压入 - O(n)， 弹出 - O(1)

![](https://pic.leetcode-cn.com/558b9e9258a8ba35c6456ea714d05f55d35da3c3306bef8fa47099093a3ab5b7-file_1561370741978)

Language: **Java**

```java
private LinkedList<Integer> q1 = new LinkedList<>();

// Push element x onto stack.
public void push(int x) {
    q1.add(x);
    int sz = q1.size();
    while (sz > 1) {
        q1.add(q1.remove());
        sz--;
    }
}
// Removes the element on top of the stack.
public int pop() {
    return q1.remove();
}
// Return whether the stack is empty.
public boolean empty() {
    return q1.isEmpty();
}
// Get the top element.
public int top() {
    return q1.peek();
}

```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/implement-stack-using-queues/solution/yong-dui-lie-shi-xian-zhan-by-leetcode/)***
