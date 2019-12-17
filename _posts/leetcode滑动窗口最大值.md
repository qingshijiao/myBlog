---
title: 239.滑动窗口最大值（Sliding Window Maximum）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [239\. 滑动窗口最大值](https://leetcode-cn.com/problems/sliding-window-maximum/)

Difficulty: **困难**


给定一个数组 _nums_，有一个大小为 _k_ 的滑动窗口从数组的最左侧移动到数组的最右侧。你只可以看到在滑动窗口内的 _k_ 个数字。滑动窗口每次只向右移动一位。

返回滑动窗口中的最大值。

**示例:**

```
输入: nums = [1,3,-1,-3,5,3,6,7], 和 k = 3
输出: [3,3,5,5,6,7]
解释:

  滑动窗口的位置                最大值
---------------               -----
[1  3  -1] -3  5  3  6  7       3
 1 [3  -1  -3] 5  3  6  7       3
 1  3 [-1  -3  5] 3  6  7       5
 1  3  -1 [-3  5  3] 6  7       5
 1  3  -1  -3 [5  3  6] 7       6
 1  3  -1  -3  5 [3  6  7]      7
```

**提示：**

你可以假设 _k_ 总是有效的，在输入数组不为空的情况下，1 ≤ k ≤ 输入数组的大小。

**进阶：**

你能在线性时间复杂度内解决此题吗？


#### Solution1 - 暴力法
最简单直接的方法是遍历每个滑动窗口，找到每个窗口的最大值。一共有 N - k + 1 个滑动窗口，每个有 k 个元素，于是算法的时间复杂度为 O(Nk)，表现较差。

Language: **Java**

```java
​class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {
        int n = nums.length;
        if (n * k == 0) return new int[0];

        int [] output = new int[n - k + 1];
        for (int i = 0; i < n - k + 1; i++) {
            int max = Integer.MIN_VALUE;
            for(int j = i; j < i + k; j++)
                max = Math.max(max, nums[j]);
            output[i] = max;
        }
        return output;
    }
}

```

#### Solution2 - 双向队列
我们可以使用双向队列，该数据结构可以从两端以常数时间压入/弹出元素。

存储双向队列的索引比存储元素更方便，因为两者都能在数组解析中使用。

Language: **Java**

```java
​class Solution {
  ArrayDeque<Integer> deq = new ArrayDeque<Integer>();
  int [] nums;

  public void clean_deque(int i, int k) {
    // remove indexes of elements not from sliding window
    if (!deq.isEmpty() && deq.getFirst() == i - k)
      deq.removeFirst();

    // remove from deq indexes of all elements
    // which are smaller than current element nums[i]
    while (!deq.isEmpty() && nums[i] > nums[deq.getLast()])                           deq.removeLast();
  }

  public int[] maxSlidingWindow(int[] nums, int k) {
    int n = nums.length;
    if (n * k == 0) return new int[0];
    if (k == 1) return nums;

    // init deque and output
    this.nums = nums;
    int max_idx = 0;
    for (int i = 0; i < k; i++) {
      clean_deque(i, k);
      deq.addLast(i);
      // compute max in nums[:k]
      if (nums[i] > nums[max_idx]) max_idx = i;
    }
    int [] output = new int[n - k + 1];
    output[0] = nums[max_idx];

    // build output
    for (int i  = k; i < n; i++) {
      clean_deque(i, k);
      deq.addLast(i);
      output[i - k + 1] = nums[deq.getFirst()];
    }
    return output;
  }
}
```

#### Solution3 - 动态规划
![](https://pic.leetcode-cn.com/e793d5c8ede0be91804b291f1565ab90c980371879d6ec683d0a05c1b4f7e984-image.png)
![](https://pic.leetcode-cn.com/4a699746334bfd5548a8a2a920e5bcd2b2922f6c39ca0bf2a52bc741a8b9c10d-image.png)
![](https://pic.leetcode-cn.com/f20d788625572649bd3def127aafdd287eb9d958fdb7e8323183980a4721f7aa-image.png)

Language: **Java**

```java
​class Solution {
  public int[] maxSlidingWindow(int[] nums, int k) {
    int n = nums.length;
    if (n * k == 0) return new int[0];
    if (k == 1) return nums;

    int [] left = new int[n];
    left[0] = nums[0];
    int [] right = new int[n];
    right[n - 1] = nums[n - 1];
    for (int i = 1; i < n; i++) {
      // from left to right
      if (i % k == 0) left[i] = nums[i];  // block_start
      else left[i] = Math.max(left[i - 1], nums[i]);

      // from right to left
      int j = n - i - 1;
      if ((j + 1) % k == 0) right[j] = nums[j];  // block_end
      else right[j] = Math.max(right[j + 1], nums[j]);
    }

    int [] output = new int[n - k + 1];
    for (int i = 0; i < n - k + 1; i++)
      output[i] = Math.max(left[i + k - 1], right[i]);

    return output;
  }
}
```

```java
class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {
        if(nums.length==0) return new int[0];
    	int res[]=new int[nums.length-k+1];
    	int max=Integer.MIN_VALUE;
    	int maxIndex=-1;
    	for(int i=0;i<=nums.length-k;i++){
    		if(i<=maxIndex){
    			if(nums[i+k-1]<max){//只与新来的比
        			res[i]=max;
    			}else{
    				max=nums[i+k-1];
    				maxIndex=i+k-1;
    				res[i]=max;
    			}

    		}else{//重新寻找
        		max=Integer.MIN_VALUE;
        		for(int j=i;j<i+k;j++){
        			if(nums[j]>max){
        				max=nums[j];
        				maxIndex=j;
        			}
        		}
        		res[i]=max;
    		}


    	}
    	return res;

    }
}
```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/sliding-window-maximum/solution/hua-dong-chuang-kou-zui-da-zhi-by-leetcode-3/)***
