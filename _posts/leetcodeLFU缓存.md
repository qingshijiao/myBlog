---
title: 460. LFU缓存（LFU Cache）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [460\. LFU缓存](https://leetcode-cn.com/problems/lfu-cache/)

Difficulty: **困难**


请你为 缓存算法设计并实现数据结构。它应该支持以下操作：`get` 和 `put`。

*   `get(key)` - 如果键存在于缓存中，则获取键的值（总是正数），否则返回 -1。
*   `put(key, value)` - 如果键已存在，则变更其值；如果键不存在，请插入键值对。当缓存达到其容量时，则应该在插入新项之前，使最不经常使用的项无效。在此问题中，当存在平局（即两个或更多个键具有相同使用频率）时，应该去除最久未使用的键。

「项的使用次数」就是自插入该项以来对其调用 `get` 和 `put` 函数的次数之和。使用次数会在对应项被移除后置为 0 。

**进阶：**  
你是否可以在 **O(1) **时间复杂度内执行两项操作？

**示例：**

```
LFUCache cache = new LFUCache( 2 /* capacity (缓存容量) */ );

cache.put(1, 1);
cache.put(2, 2);
cache.get(1);       // 返回 1
cache.put(3, 3);    // 去除 key 2
cache.get(2);       // 返回 -1 (未找到key 2)
cache.get(3);       // 返回 3
cache.put(4, 4);    // 去除 key 1
cache.get(1);       // 返回 -1 (未找到 key 1)
cache.get(3);       // 返回 3
cache.get(4);       // 返回 4
```


#### Solution

Language: **Java**

```java
​class LFUCache {

    private Map<Integer, ListNode> map; // key --> 题目中的key； value --> ListNode
    private Map<Integer, DoubleLinkedList> frequencyMap; // 访问次数哈希表，使用 ListNode[] 也可以，不过要占用很多空间
    private Integer capacity; // 外部传入容量的大小
    private Integer maxFrequency = 1; // 全局最高访问次数，删除最少使用访问次数的结点时会用到

    public LFUCache(int capacity) {
        map = new HashMap<>(capacity);
        frequencyMap = new HashMap<>();
        this.capacity = capacity;
    }

    // get 一次操作，访问次数就增加 1；
    // 从原来的链表调整到访问次数更高的链表的表头
    public int get(int key) {
        // corner case
        if (capacity == 0) return -1; // 测试测出来的，capacity 可能传 0

        //每次访问一个已经存在的元素的时候：
        // 应该先把结点类从当前所属的访问次数双链表里删除，然后再添加到它「下一个访问次数」的双向链表的头部；
        if (map.containsKey(key)) {
            ListNode node = removeListNode(key);
            int frequency = node.frequency;
            addListNodeToHead(frequency, node);
            return node.value;
        } else {
            return -1;
        }
    }

    public void put(int key, int value) {
        // 如果 key 存在，就更新访问次数 + 1，更新值
        if (map.containsKey(key)) {
            ListNode node = removeListNode(key);
            node.value = value;
            int frequency = node.frequency;
            addListNodeToHead(frequency, node);
            return;
        }

        // 如果 key 不存在
        // 1、如果满了，先删除访问次数最小的的末尾结点，再删除 map 里对应的 key
        if (map.size() == capacity) {
            for (int i = 1; i <= maxFrequency; i++) {
                if (frequencyMap.containsKey(i) && frequencyMap.get(i).count > 0) {
                    // 1、从双链表里删除结点
                    DoubleLinkedList doubleLinkedList = frequencyMap.get(i);
                    ListNode removeNode = doubleLinkedList.removeTail();

                    // 2、删除 map 里对应的 key
                    map.remove(removeNode.key);
                    break;
                }
            }
        }

        // 2、再创建新结点放在访问次数为 1 的双向链表的前面
        ListNode newNode = new ListNode(key, value);
        addListNodeToHead(1, newNode);
        map.put(key, newNode);
    }

    // 以下部分主要是结点类和双向链表的操作
    // 结点类，是双向链表的组成部分
    private class ListNode {
        private int key;
        private int value;
        private int frequency = 1;
        private ListNode pre;
        private ListNode next;

        public ListNode() {

        }

        public ListNode(int key, int value) {
            this.key = key;
            this.value = value;
        }
    }

    // 双向链表
    private class DoubleLinkedList {
        private ListNode dummyHead; // 虚拟头结点，它无前驱结点
        private ListNode dummyTail; // 虚拟尾结点，它无后继结点
        private int count; // 当前双向链表的有效结点数

        public DoubleLinkedList() {
            this.dummyHead = new ListNode(-1, -1);
            this.dummyTail = new ListNode(-1, -1);

            dummyHead.next = dummyTail;
            dummyTail.pre = dummyHead;
            count = 0;
        }

        // 把一个结点类添加到双向链表的开头（头部是最新使用数据）
        public void addNodeToHead(ListNode addNode) {
            ListNode oldNode = dummyHead.next;
            dummyHead.next = addNode;
            addNode.next = oldNode;
            addNode.pre = dummyHead;
            oldNode.pre = addNode;
            count++;
        }

        // 把双向链表的末尾结点删除（尾部是最旧的数据，在缓存满的时候淘汰）
        public ListNode removeTail() {
            ListNode oldTail = dummyTail.pre;
            ListNode newTail = oldTail.pre;

            newTail.next = dummyTail;
            dummyTail.pre = newTail;

            oldTail.next = null;
            oldTail.pre = null;
            count--;
            return oldTail;
        }
    }

    // 将原来访问次数的结点，从双向链表里脱离出来
    private ListNode removeListNode(int key) {
        ListNode deleteNode = map.get(key);
        ListNode preNode = deleteNode.pre;
        ListNode nextNode = deleteNode.next;

        preNode.next = nextNode;
        nextNode.pre = preNode;

        deleteNode.pre = null;
        deleteNode.next = null;

        // 维护双链表结点数
        frequencyMap.get(deleteNode.frequency).count--;
        // 访问次数+1
        deleteNode.frequency++;
        maxFrequency = Math.max(maxFrequency, deleteNode.frequency);

        return deleteNode;
    }

    // 把结点放在对应访问次数的双向链表的头部
    private void addListNodeToHead(int frequency, ListNode addNode) {
        DoubleLinkedList doubleLinkedList;

        // 如果不存在，就初始化
        if (frequencyMap.containsKey(frequency)) {
            doubleLinkedList = frequencyMap.get(frequency);
        } else {
            doubleLinkedList = new DoubleLinkedList();
        }

        doubleLinkedList.addNodeToHead(addNode);
        frequencyMap.put(frequency, doubleLinkedList);
    }
}

/**
 * Your LFUCache object will be instantiated and called as such:
 * LFUCache obj = new LFUCache(capacity);
 * int param_1 = obj.get(key);
 * obj.put(key,value);
 */
```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/lfu-cache/)***
