---
title: 232.用栈实现队列（Implement Queue using Stacks）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [232\. 用栈实现队列](https://leetcode-cn.com/problems/implement-queue-using-stacks/)

Difficulty: **简单**


使用栈实现队列的下列操作：

*   push(x) -- 将一个元素放入队列的尾部。
*   pop() -- 从队列首部移除元素。
*   peek() -- 返回队列首部的元素。
*   empty() -- 返回队列是否为空。

**示例:**

```
MyQueue queue = new MyQueue();

queue.push(1);
queue.push(2);
queue.peek();  // 返回 1
queue.pop();   // 返回 1
queue.empty(); // 返回 false
```

**说明:**

*   你只能使用标准的栈操作 -- 也就是只有 `push to top`, `peek/pop from top`, `size`, 和 `is empty` 操作是合法的。
*   你所使用的语言也许不支持栈。你可以使用 list 或者 deque（双端队列）来模拟一个栈，只要是标准的栈操作即可。
*   假设所有操作都是有效的 （例如，一个空的队列不会调用 pop 或者 peek 操作）。


#### Solution1 - 使用两个栈 入队 - O(n)， 出队 - O(1)
![](https://pic.leetcode-cn.com/c631edf5bdffe4fb3f9708d1d7ee70e992c1afe17563445b7b29f2686384a2b7-file_1561371337486)
Language: **Java**

```java
​private int front;

public void push(int x) {
    if (s1.empty())
        front = x;
    while (!s1.isEmpty())
        s2.push(s1.pop());
    s2.push(x);
    while (!s2.isEmpty())
        s1.push(s2.pop());
}

// Removes the element from the front of queue.
public void pop() {
    s1.pop();
    if (!s1.empty())
        front = s1.peek();
}

// Return whether the queue is empty.
public boolean empty() {
    return s1.isEmpty();
}

// Get the front element.
public int peek() {
  return front;
}
```

#### Solution2 - 使用两个栈 入队 - O(1)，出队 - 摊还复杂度 O(1)
一个栈用作入队，另一个栈用作出队
![](https://pic.leetcode-cn.com/b7ee1de51cf97d3e6ae445682de13b9495e51f9b91a802b77a89f700035e7945-file_1561371337486)
![](https://pic.leetcode-cn.com/b7ee1de51cf97d3e6ae445682de13b9495e51f9b91a802b77a89f700035e7945-file_1561371337486)
Language: **Java**

```java
​class MyQueue {
        Stack<Integer> stackB;
        Stack<Integer> stackA;
        int size;
        /** Initialize your data structure here. */
        public MyQueue() {
            stackA=new Stack<>();
            stackB=new Stack<>();
            size=0;
        }

        /** Push element x to the back of queue. */
        public void push(int x) {
            stackA.push(x);size++;
        }

        /** Removes the element from in front of queue and returns that element. */
        public int pop() {
            if(stackB.isEmpty())
            {
                while (!stackA.isEmpty())
                {
                    stackB.push(stackA.pop());

                }
            }
            if(size>0)size--;
            else return -1;
            return stackB.pop();
        }

        /** Get the front element. */
        public int peek() {
            if(stackB.isEmpty())
            {
                while (!stackA.isEmpty())
                {
                    stackB.push(stackA.pop());
                }
            }
            if(size>0)return stackB.peek();
            return -1;
        }

        /** Returns whether the queue is empty. */
        public boolean empty() {
            if(size<=0)return true;
            else return false;
        }
    }

/**
 * Your MyQueue object will be instantiated and called as such:
 * MyQueue obj = new MyQueue();
 * obj.push(x);
 * int param_2 = obj.pop();
 * int param_3 = obj.peek();
 * boolean param_4 = obj.empty();
 */
```


---
***参考：
[LeetCode](https://leetcode-cn.com/problems/implement-queue-using-stacks/solution/yong-zhan-shi-xian-dui-lie-by-leetcode/)***
