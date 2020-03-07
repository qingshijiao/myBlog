---
title: 281.锯齿迭代器

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [281\.锯齿迭代器](https://leetcode-cn.com/problems/zigzag-iterator/)

Difficulty: **中等**

给出两个一维的向量，请你实现一个迭代器，交替返回它们中间的元素。

示例:
```
输入:
v1 = [1,2]
v2 = [3,4,5,6]

输出:
[1,3,2,4,5,6]

解析:
 通过连续调用 next 函数直到 hasNext 函数返回false，
next 函数返回值的次序应依次为: [1,3,2,4,5,6]。
```

**拓展**：假如给你 k 个一维向量呢？你的代码在这种情况下的扩展性又会如何呢?

**拓展声明：**
 “锯齿” 顺序对于 k > 2 的情况定义可能会有些歧义。所以，假如你觉得 “锯齿” 这个表述不妥，也可以认为这是一种 “循环”。例如：
```
输入:
[1,2,3]
[4,5,6,7]
[8,9]

输出:
[1,4,8,2,5,9,3,6,7]
```


#### Solution1 - 合并

Language: **python**

```python

class ZigzagIterator(object):

    def __init__(self, v1, v2):
        """
        Initialize your data structure here.
        :type v1: List[int]
        :type v2: List[int]
        """
        self.list = []
        if v1 and v2:
            i = 0
            for i in range(min(len(v1), len(v2))):
                self.list.append(v1[i])
                self.list.append(v2[i])
            if v1[i + 1:]:
                self.list += v1[i + 1:]
            else:
                self.list += v2[i + 1:]

        elif v1:
            self.list = v1
        else:
            self.list = v2
        self.index = 0
    def next(self):
        """
        :rtype: int
        """
        self.index += 1
        return self.list[self.index - 1]

    def hasNext(self):
        """
        :rtype: bool
        """
        return self.index != len(self.list)


# Your ZigzagIterator object will be instantiated and called as such:
# i, v = ZigzagIterator(v1, v2), []
# while i.hasNext(): v.append(i.next())
```

#### Solution2 - 下标扫描

Language: **python**

```python
class ZigzagIterator(object):

    def __init__(self, v1, v2):
        """
        Initialize your data structure here.
        :type v1: List[int]
        :type v2: List[int]
        """
        self.i1, self.i2 = 0, 0
        self.v1, self.v2 = v1, v2
        self.indicator = 0 # 0 for v1, 1 for v2

    def next(self):
        """
        :rtype: int
        """
        if not self.indicator:
            self.indicator = 1
            if self.i1 < len(self.v1):
                self.i1 += 1
                return self.v1[self.i1 - 1]
            else:
                self.i2 += 1
                return self.v2[self.i2 - 1]
        else:
            self.indicator = 0
            if self.i2 < len(self.v2):
                self.i2 += 1
                return self.v2[self.i2 - 1]
            else:
                self.i1 += 1
                return self.v1[self.i1 - 1]

    def hasNext(self):
        """
        :rtype: bool
        """
        return self.i1 < len(self.v1) or self.i2 < len(self.v2)

# Your ZigzagIterator object will be instantiated and called as such:
# i, v = ZigzagIterator(v1, v2), []
# while i.hasNext(): v.append(i.next())
```


---
***参考：
[暴躁老哥在线刷题](https://blog.csdn.net/qq_32424059/article/details/90517554)***
