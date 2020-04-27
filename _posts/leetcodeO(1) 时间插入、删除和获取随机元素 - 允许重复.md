---
title: 381.O(1) 时间插入、删除和获取随机元素 - 允许重复 (Insert Delete GetRandom O(1) - Duplicates allowed)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [381\. O(1) 时间插入、删除和获取随机元素 - 允许重复](https://leetcode-cn.com/problems/insert-delete-getrandom-o1-duplicates-allowed/)

Difficulty: **困难**


设计一个支持在_平均 _时间复杂度 **O(1) **下**， **执行以下操作的数据结构。

**注意: 允许出现重复元素。**

1.  `insert(val)`：向集合中插入元素 val。
2.  `remove(val)`：当 val 存在时，从集合中移除一个 val。
3.  `getRandom`：从现有集合中随机获取一个元素。每个元素被返回的概率应该与其在集合中的数量呈线性相关。

**示例:**

```
// 初始化一个空的集合。
RandomizedCollection collection = new RandomizedCollection();

// 向集合中插入 1 。返回 true 表示集合不包含 1 。
collection.insert(1);

// 向集合中插入另一个 1 。返回 false 表示集合包含 1 。集合现在包含 [1,1] 。
collection.insert(1);

// 向集合中插入 2 ，返回 true 。集合现在包含 [1,1,2] 。
collection.insert(2);

// getRandom 应当有 2/3 的概率返回 1 ，1/3 的概率返回 2 。
collection.getRandom();

// 从集合中删除 1 ，返回 true 。集合现在包含 [1,2] 。
collection.remove(1);

// getRandom 应有相同概率返回 1 和 2 。
collection.getRandom();
```


#### Solution

Language: **Java**

```java
​class RandomizedCollection {

   List<Integer> list = new ArrayList<>();
    Map<Integer,List<Integer>> map = new HashMap<>();
    Random random = new Random();
    /** Initialize your data structure here. */
    public RandomizedCollection() {

    }

    /** Inserts a value to the collection. Returns true if the collection did not already contain the specified element. */
    public boolean insert(int val) {
        if(!map.containsKey(val)){
            List<Integer> l = new ArrayList<>();
            l.add(list.size());
            map.put(val,l);
            list.add(val);
            return true;
        }else {
            map.get(val).add(list.size());
            list.add(val);
            return false;
        }
    }

    /** Removes a value from the collection. Returns true if the collection contained the specified element. */
    public boolean remove(int val) {
        if(!map.containsKey(val))return false;
        else {
            List<Integer> l = map.get(val);
            int last = list.get(list.size()-1);
            if(last==val){
                //直接删除尾部
                list.remove(list.size()-1);
                l.remove(l.size()-1);
                if(l.size()==0)map.remove(val);
            }else {
                int lastposition = list.size()-1;
                int position = l.get(l.size()-1);
                l.remove(l.size()-1);
                if(l.size()==0)map.remove(val);
                list.set(position,last);
                list.remove(list.size()-1);
                List<Integer> last_list = map.get(last);
                for(int i=0;i<last_list.size();i++){
                    if(last_list.get(i)==lastposition)last_list.set(i,position);
                }
            }
            return true;
        }
    }

    /** Get a random element from the collection. */
    public int getRandom() {
        return list.get(random.nextInt(list.size()));
    }
}

/**
 * Your RandomizedCollection object will be instantiated and called as such:
 * RandomizedCollection obj = new RandomizedCollection();
 * boolean param_1 = obj.insert(val);
 * boolean param_2 = obj.remove(val);
 * int param_3 = obj.getRandom();
 */
```

---
***参考:
[leetcode](https://leetcode-cn.com/problems/insert-delete-getrandom-o1-duplicates-allowed/submissions/)***
