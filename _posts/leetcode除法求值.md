---
title: 399.除法求值 (Evaluate Division)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [399\. 除法求值](https://leetcode-cn.com/problems/evaluate-division/)

Difficulty: **中等**


给出方程式 `A / B = k`, 其中 `A` 和 `B` 均为代表字符串的变量， `k` 是一个浮点型数字。根据已知方程式求解问题，并返回计算结果。如果结果不存在，则返回 `-1.0`。

**示例 :**
给定 `a / b = 2.0, b / c = 3.0`
问题: `a / c = ?, b / a = ?, a / e = ?, a / a = ?, x / x = ? `
返回 `[6.0, 0.5, -1.0, 1.0, -1.0 ]`

输入为: `vector<pair<string, string>> equations, vector<double>& values, vector<pair<string, string>> queries`(方程式，方程式结果，问题方程式)， 其中 `equations.size() == values.size()`，即方程式的长度与方程式结果长度相等（程式与结果一一对应），并且结果值均为正数。以上为方程式的描述。 返回`vector<double>`类型。

基于上述例子，输入如下：

```
equations(方程式) = [ ["a", "b"], ["b", "c"] ],
values(方程式结果) = [2.0, 3.0],
queries(问题方程式) = [ ["a", "c"], ["b", "a"], ["a", "e"], ["a", "a"], ["x", "x"] ].
```

输入总是有效的。你可以假设除法运算中不会出现除数为0的情况，且不存在任何矛盾的结果。


#### Solution

Language: **Java**

```java
​import java.util.*;

class Solution {

    private Map<String, Node> graph = new HashMap<>();

    public double[] calcEquation(List<List<String>> equations, double[] values,
                                 List<List<String>> queries) {

        for (int i = 0; i < equations.size(); i++) {
            constructGraph(equations.get(i), values[i]);
        }
        double[] ans = new double[queries.size()];
        for (int i = 0; i < queries.size(); i++) {
            List<String> query = queries.get(i);
            ans[i] = result(query.get(0),query.get(1));
        }
        return ans;
    }

    private void constructGraph(List<String> a_divide_b,
                                double quotient) {
        String a = a_divide_b.get(0);
        String b = a_divide_b.get(1);
        Node aNode = graph.get(a);
        Node bNode = graph.get(b);
        if (aNode == null && bNode == null) {
            bNode = new Node(1d, b);
            graph.put(b, bNode);
            aNode = new Node(quotient, b);
            graph.put(a, aNode);
        } else if (aNode != null && bNode != null) {
            reverse(a);
            aNode.parent = b;
            aNode.val = quotient;
        } else if (aNode == null) {
            aNode = new Node(quotient, b);
            graph.put(a, aNode);
        } else if (bNode == null) {
            bNode = new Node(1 / quotient, a);
            graph.put(b, bNode);
        }
    }

    private void reverse(String now) {
        Node nowNode = graph.get(now);
        if (now.equals(nowNode.parent)) return;
        reverse(nowNode.parent);
        Node parNode = graph.get(nowNode.parent);
        parNode.parent = now;
        parNode.val = 1 / nowNode.val;
    }

    private Pair findFinal(String p, double valArrivaRoot) {
        Node node = graph.get(p);
        if (node == null) return null;
        if (!p.equals(node.parent)) {
            return findFinal(node.parent, valArrivaRoot * node.val);
        } else {
            return new Pair(p, valArrivaRoot);
        }
    }

    private double result(String a, String b) {
        Pair aFinal = findFinal(a, 1d);
        Pair bFinal = findFinal(b, 1d);
        if (aFinal == null || bFinal == null) return -1;
        if (!aFinal.root.equals(bFinal.root)) return -1;
        return aFinal.value / bFinal.value;
    }

    class Node {
        public double val;
        public String parent;

        public Node(double val, String parent) {
            this.val = val;
            this.parent = parent;
        }
    }

    class Pair {
        public String root;
        public double value;

        public Pair(String root, double value) {
            this.root = root;
            this.value = value;
        }
    }
}
```

---
***参考:
[leetcode](https://leetcode-cn.com/problems/evaluate-division/submissions/)***
