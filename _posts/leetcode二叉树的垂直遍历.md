---
title: 313.超级丑数 (Super Ugly Number)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
给定二叉树，按垂序遍历返回其结点值。
对位于 (X, Y) 的每个结点而言，其左右子结点分别位于 (X-1, Y-1) 和 (X+1, Y-1)。
把一条垂线从 X = -infinity 移动到 X = +infinity ，每当该垂线与结点接触时，我们按从上到下的顺序报告结点的值（ Y 坐标递减）。
如果两个结点位置相同，则首先报告的结点值较小。
按 X 坐标顺序返回非空报告的列表。每个报告都有一个结点值列表。

![](https://img-blog.csdnimg.cn/20190621112642252.png)

```
输入：[3,9,20,null,null,15,7]
输出：[[9],[3,15],[20],[7]]
解释：
在不丧失其普遍性的情况下，我们可以假设根结点位于 (0, 0)：
然后，值为 9 的结点出现在 (-1, -1)；
值为 3 和 15 的两个结点分别出现在 (0, 0) 和 (0, -2)；
值为 20 的结点出现在 (1, -1)；
值为 7 的结点出现在 (2, -2)。
```

#### Solution

Language: **Java**

```java
​/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
	//这个HashMap是实现的关键，它就是我们分类的映射
	//key：x 也就是以x对应的值为一类
	//value： List<Entry> 这个list对应同一类的Entry
	//Entry: 包装以X分类好之后每个结点的信息，成员变量有y和结点值val
   HashMap<Integer, List<Entry>> map = new HashMap<>();

    public List<List<Integer>> verticalTraversal(TreeNode root) {
    	//re:返回结果
        List<List<Integer>> re = new ArrayList<>();
        //调用遍历二叉树方法，在遍历的同时以X值进行了分类
        //也就是说在这个方法之后，HashMap中已经有了数据
        iterateTreeNode(root,0,0);
        //得到所有的x
        Object[] objects = map.keySet().toArray();
         //在分类之后对X的值进行升序排序
        Arrays.sort(objects);
        //依照升序的x值遍历整个结果，并且对每个分类进行内部排序
        for (Object key: objects
             ) {
             //得到一类的数组
            List<Entry> list = map.get(key);
            //对该组数据进行排序
            list.sort(new Comparator<Entry>() {
                @Override
                //排序逻辑
                public int compare(Entry o1, Entry o2) {
                	//y不相等，直接以Y的降序进行排序，大的在前面
                   if (o1.y != o2.y)
                        return Integer.compare(o2.y,o1.y) ;
                    //如果y相等，那就依照value值进行排序，它是升序，小的在前面
                    else
                        return Integer.compare(o1.val,o2.val) ;
                }
            });
          	//经过上面的排序后，我们提取出val值，因为我们最后结果只需要val值
            List<Integer> integerList = new ArrayList<>() ;
            for (Entry entry:list){
            	//添加到integer数组中
                integerList.add(entry.val) ;
            }
            把integerList加到结果值中
            re.add(integerList) ;
        }
        //返回结果
        return re ;
    }
    //遍历二叉树方法
    private void iterateTreeNode(TreeNode node,int x, int y){
    	//递归出口
        if (node == null)
            return;
         //如果有该类则直接把Entry加进去
        if (map.containsKey(x)){
            map.get(x).add(new Entry(node.val,y));
        }
        //没有该分类，即创建该分类，并加入对应的List<Entry>
        else
            map.put(x,new java.util.ArrayList<>(Arrays.asList(new Entry(node.val,y)))) ;
        //递归左子节点
        iterateTreeNode(node.left,x-1,y-1);
        //递归右子节点
        iterateTreeNode(node.right,x+1,y-1);
    }
    //定义的内部类，用来辅助我们保存信息的
    class Entry  {
    	//结点值
        int val;
        //Y值
        int y ;
		//只有一个构造方法
        public Entry(int val, int y) {
            this.val = val;
            this.y = y;
        }
}
}

```

---
***参考：
[weixin_43092168](https://blog.csdn.net/weixin_43092168/article/details/93176238)***
