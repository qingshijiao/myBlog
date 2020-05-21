---
title: 432. 全 O(1) 的数据结构 (All O`one Data Structure)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [432\. 全 O(1) 的数据结构](https://leetcode-cn.com/problems/all-oone-data-structure/)

Difficulty: **困难**


请你实现一个数据结构支持以下操作：

1.  `Inc(key)` - 插入一个新的值为 1 的 key。或者使一个存在的 key 增加一，保证 key 不为空字符串。
2.  `Dec(key)` - 如果这个 key 的值是 1，那么把他从数据结构中移除掉。否则使一个存在的 key 值减一。如果这个 key 不存在，这个函数不做任何事情。key 保证不为空字符串。
3.  `GetMaxKey()` - 返回 key 中值最大的任意一个。如果没有元素存在，返回一个空字符串`""` 。
4.  `GetMinKey()` - 返回 key 中值最小的任意一个。如果没有元素存在，返回一个空字符串`""`。

**挑战：**

你能够以 O(1) 的时间复杂度实现所有操作吗？


#### Solution

Language: **Java**

```java
​class AllOne {

    /** Initialize your data structure here. */
    public AllOne() {

    }
    IncrQueue q = new IncrQueue();
    /** Inserts a new key <Key> with value 1. Or increments an existing key by 1. */
    public void inc(String key) {
            q.inc(key);
    }
    
    /** Decrements an existing key by 1. If Key's value is 1, remove it from the data structure. */
    public void dec(String key) {
            q.dec(key);
    }
    
    /** Returns one of the keys with maximal value. */
    public String getMaxKey() {
       return q.getMaxKey();
    }
    
    /** Returns one of the keys with Minimal value. */
    public String getMinKey() {
        return q.getMinKey();
    }


    public static class IncrQueue {

        private Node head,tail;
        private Map<String,Node> map=new HashMap<>();


        //再使用两个结点来 保存最大结点和最小结点？


        private Node newNode(String key,int v){
            Node node = new Node();
            node.key=key;
            node.value=v;
            return node;
        }


        private static class Node{
            String key;
            int value;
            Node next;
            Node prex;
        }
  private void afterIncr (Node node) {
            Node p = node.prex;
            Node n = node.next;
            //空出连接
            if ( node.value >= head.value && node != head ) {
                node.prex = node.next = null;
                if ( node == tail ) {
                    this.tail = p;
                    this.tail.next = null;
                } else {
                    //断开连接
                    p.next = n;
                    n.prex = p;
                }
                node.next = head;
                head.prex = node;
                this.head = node;
            } else if ( node != head ) {

                if ( node != tail ) {
                    if ( node != head.next && node.value < p.value  ) {
                        p.next = n;
                        n.prex = p;
                        node.prex = head;
                        node.next = head.next;
                        node.next.prex = node;
                        head.next = node;
                    }
                } else {
                    Node pp = p.prex;
                    if ( pp!=null ){
                        pp.next = node;
                        node.prex = pp;
                        node.next = p;
                        p.next = null;
                        this.tail = p;
                    }
                }
            }
            
        }
        private void updateInc(Node node){
          afterIncr(node);
        }

        private void updateDec(Node node){
            Node tai = this.tail;
      
        
                if ( node.value<tai.value){
                    //断开连接。
                    Node p = node.prex;
                    Node n = node.next;
                    if ( p!=null){
                        p.next=n;
                    }
                    if ( n!=null){
                        n.prex=p;
                    }
                    //重新构建连接。
                    //
                    node.prex=tai;
                    this.tail=node;
                }

    
        }


        public void inc (String key) {
            Node node = map.get(key);
            if ( node==null){
                node=newNode(key,1);
                map.put(key,node);
                // 这里 和下面都需要单独判断
                //判断是否大于尾部结点。
                Node t = this.tail;
                if ( t==null){
                    this.head=this.tail=node;
                }else {
                    node.prex=t;
                    t.next=node;
                    this.tail=node;
                }
            }else {
                node.value +=1;
                updateInc(node);
            }

        }

        private void unlinkNode(Node node){
            Node p = node.prex;
            Node n = node.next;
            node.prex=node.next=null;
            if ( n!=null){
                n.prex=p;
                if ( p!=null ) p.next=n;
                 else this.head=n;
            }else{
                //现在删除的尾部元素。
                this.tail=p;
                if ( p==null){
                    this.head=null;
                }else p.next=null;
            }
        }


        public void dec (String key) {
            Node node = map.get(key);
            if ( node!=null){
                if ( node.value==1){
                    //从映射表中删除。
                    //之后断开连接
                    map.remove(key);
                    unlinkNode(node);
                }else {
                    node.value -=1;
                    updateDec(node);
                }

            }
        }

        /**
         * Returns one of the keys with maximal value.
         */
        public String getMaxKey () {
            return this.head!=null?head.key:"";

        }

        /**
         * Returns one of the keys with Minimal value.
         */
        public String getMinKey () {
            return this.tail!=null?tail.key:"";
        }
    }
}

/**
 * Your AllOne object will be instantiated and called as such:
 * AllOne obj = new AllOne();
 * obj.inc(key);
 * obj.dec(key);
 * String param_3 = obj.getMaxKey();
 * String param_4 = obj.getMinKey();
 */
```

---
***参考：
[leetcode](https://leetcode-cn.com/problems/all-oone-data-structure/submissions/)***
