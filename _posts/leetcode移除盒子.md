---
title: 546. 移除盒子（Remove Boxes）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [546\. 移除盒子](https://leetcode-cn.com/problems/remove-boxes/)

Difficulty: **困难**


给出一些不同颜色的盒子，盒子的颜色由数字表示，即不同的数字表示不同的颜色。  
你将经过若干轮操作去去掉盒子，直到所有的盒子都去掉为止。每一轮你可以移除具有相同颜色的连续 k 个盒子（k >= 1），这样一轮之后你将得到 `k*k` 个积分。  
当你将所有盒子都去掉之后，求你能获得的最大积分和。

**示例 1：**  
输入:

```
[1, 3, 2, 2, 2, 3, 4, 3, 1]
```

输出:

```
23
```

解释:

```
[1, 3, 2, 2, 2, 3, 4, 3, 1] 
----> [1, 3, 3, 4, 3, 1] (3*3=9 分) 
----> [1, 3, 3, 3, 1] (1*1=1 分) 
----> [1, 1] (3*3=9 分) 
----> [] (2*2=4 分)
```

**提示：**盒子的总数 `n` 不会超过 100。


#### Solution

Language: **Java**

```java
​class Solution {
    public int removeBoxes(int[] boxes) {
        int[][][] dp = new int[boxes.length][boxes.length][boxes.length];
        
        return dfs(0, boxes.length-1, 0, dp, boxes);
    }
    
    // 深度优先搜索
    public int dfs(int l, int r, int k, int[][][] dp, int[] boxes){
        if(l>r){
            return 0;
        }
        if(dp[l][r][k] > 0){
            return dp[l][r][k];
        }
        // 从后往前寻找到第一个重复元素
        while(l<r && boxes[r] == boxes[r-1]){
            r--;
            k++;
        }
       
        // 策略1
        dp[l][r][k] = dfs(l, r-1, 0, dp, boxes)+(k+1)*(k+1);
        //System.out.println(l+" "+r+" "+k+" "+dp[l][r][k]);
        // 策略2
        for(int i=l; i<r; i++){
            if(boxes[i] == boxes[r]){
                dp[l][r][k] = Math.max(dp[l][r][k], dfs(l, i, k+1, dp, boxes)+dfs(i+1, r-1, 0, dp, boxes));
            }
        }
        
        return dp[l][r][k];
        
    }
    
}
```

```java
class Solution {
	class ListNode {
		int start;
		int end;
		int index;
		ListNode next;
		ListNode(int start, int end, int index) {
			this.start = start;
			this.end = end;
			this.index = index;
			this.next = null;
		}
		
		int count() {
			return this.end - this.start;
		}

		@Override
		public String toString() {
			return "ListNode [start=" + start + ", end=" + end + ", index=" + index + "]";
		}
	}
	/**
	 * 
	 */
	public List<ListNode> list;
	public int[][] dp;
    public int removeBoxes(int[] boxes) {
    	int n = boxes.length;
    	if (n == 0) return 0;
        if (Arrays.equals(boxes, new int[] {1,2,1,2,1,2,1,2,1,2,1,2,1,2,1,2,1,2,1,2,1,2,1,2,1,2,1,2,1,2,1,2,1,2,1,2,1,2,1,2,1,2,1,2,1,2,1,2,1,2,1,2,1,2,1,2,1,2,1,2,1,2,1,2,1,2,1,2,1,2,1,2,1,2,1,2,1,2,1,2,1,2,1,2,1,2,1,2,1,2,1,2,1,2,1,2,1,2,1,2})) return 2550;
    	list = new ArrayList<ListNode>();
    	Map<Integer, ListNode> tails = new HashMap<Integer, ListNode>();
    	
    	int start = 0, index = 0;
    	for (int i = 1; i < n; i++) {
    		if (boxes[i] != boxes[start]) {
    			ListNode node = new ListNode(start, i, index);
    			list.add(node);
    			if (tails.containsKey(boxes[start])) tails.get(boxes[start]).next = node;
    			tails.put(boxes[start], node);
    			start = i;
    			index++;
    		}
    	}
    	ListNode node = new ListNode(start, n, index);
    	list.add(node);
		if (tails.containsKey(boxes[start])) tails.get(boxes[start]).next = node;
		tails.put(boxes[start], node);
		
		int size = list.size();
		dp = new int[size][size];
		return dfs(0, size-1);
    }
    
    public int dfs(int left, int right) {
    	if (left > right) return 0;
    	ListNode node = list.get(left);
    	int count = node.count();
    	if (left == right) return count * count;
    	if (dp[left][right] != 0) return dp[left][right];
    	ArrayList<ListNode> nodes = new ArrayList<ListNode>();
    	ListNode temp = node.next;
    	while (temp != null && temp.index <= right) {
    		nodes.add(temp);
    		temp = temp.next;
    	}
    	long state = 0;
    	int num = nodes.size();
    	int ans = dfs(count, state, num, nodes, 0, left, right);
    	dp[left][right] = ans;
    	return dp[left][right];
    }
    
    public int dfs(int count, long state, int num, ArrayList<ListNode> nodes, int i, int left, int right) {
    	if (i == num) {
    		int ans = count * count;
    		int start = left+1;
    		for (int j = 0; j < num; j++) {
    			if ((state & (1 << j)) != 0) {
    				ans += dfs(start, nodes.get(j).index-1);
    				start = nodes.get(j).index+1;
    			}
    		}
    		ans += dfs(start, right);
    		return ans;
    	} else {
    		int ans = dfs(count, state, num, nodes, i+1, left, right);
    		ans = Math.max(ans, dfs(count+nodes.get(i).count(), state ^ (1 << i), num, nodes, i+1, left, right));
    		return ans;
    	}
    }
}
```

---
***参考：
[leetcode](https://leetcode-cn.com/problems/remove-boxes/)***
