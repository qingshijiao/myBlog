---
title: 18.四数之和（4Sum）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给定一个包含 n 个整数的数组 nums 和一个目标值 target，判断 nums 中是否存在四个元素 a，b，c 和 d ，使得 a + b + c + d 的值与 target 相等？找出所有满足条件且不重复的四元组。

**注意：**
答案中不可以包含重复的四元组。

示例：
```
给定数组 nums = [1, 0, -1, 0, -2, 2]，和 target = 0。

满足要求的四元组集合为：
[
  [-1,  0, 0, 1],
  [-2, -1, 1, 2],
  [-2,  0, 0, 2]
]
```

# 题解

## 官方题解
暂无

## 其他题解
### 1.双指针
**思路：** 几数之和的思路都是一样的，先固定一个或几个数，然后用双指针查找。
这里是固定两个数

```
class Solution {
  public List<List<Integer>> fourSum(int[] nums, int target) {

        List<List<Integer>> result = new ArrayList<>();
        //先排序
        Arrays.sort(nums);

        for (int i = 0;i < nums.length - 2;i ++) {
            // 去除指针i可能的重复情况
            if (i != 0 && nums[i] == nums[i-1]) {
                continue;
            }
            for (int j = i + 1;j < nums.length;j ++) {
                // 去除j可能重复的情况
                if (j != i + 1 && nums[j] == nums[j-1]) {
                    continue;
                }

                int left = j + 1;
                int right = nums.length -1;

                while (left < right) {
                    // 不满足条件或者重复的，继续遍历
                    if ((left != j + 1 && nums[left] == nums[left-1]) || nums[i] + nums[j] + nums[left] + nums[right] < target) {
                        left ++;
                    } else if ((right != nums.length -1 && nums[right] == nums[right + 1]) || nums[i] + nums[j] + nums[left] + nums[right] > target) {
                        right --;
                    } else {
                        List<Integer> list = new ArrayList<>();
                        list.add(nums[i]);
                        list.add(nums[j]);
                        list.add(nums[left]);
                        list.add(nums[right]);

                        result.add(list);
                        // 满足条件的，进入下一次遍历
                        left ++;
                        right --;
                    }
                }

            }
        }

        return result;
    }
}

```

### 2.递归
**思路：** 解决k数之和的统一方法，将k数之和递归为两数之和然后利用双指针解决。
```
class Solution {
    public List<List<Integer>> fourSum(int[] nums, int target) {
        //对数组先排序
        Arrays.sort(nums);
        return kSum(nums, target, 4, 0);
    }

    public static ArrayList<List<Integer>> kSum(int nums[],int target,int k, int start){
        ArrayList<List<Integer>> res = new ArrayList<List<Integer>>();
        if(start>=nums.length)
            return res;
        if(k==2){
            int l = start, h = nums.length-1;
            while(l<h){
                if(nums[l]+nums[h]==target){
                    List<Integer> list = new ArrayList<>();
                    list.add(nums[l]);
                    list.add(nums[h]);
                    res.add(list);
                    while(l<h&&nums[l]==nums[l+1])
                        l++;
                    while(l<h&&nums[h]==nums[h-1])
                        h--;
                    l++;
                    h--;
                }else if(nums[l]+nums[h]<target)
                    l++;
                else
                    h--;
            }
            return res;
        }
        if(k>2){
            for(int i=start;i<nums.length-k+1;i++){
                ArrayList<List<Integer>> temp = kSum(nums, target - nums[i], k - 1, i + 1);
                if(temp!=null) {
                    for (List<Integer> l : temp) {
                        l.add(0, nums[i]);
                    }
                    res.addAll(temp);
                }
                while(i<nums.length-1&&nums[i]==nums[i+1]){
                    i++;
                }
            }
            return res;
        }
        return res;
    }

}
```


---
***参考：
[meng-chui-lu](https://leetcode-cn.com/problems/two-sum/solution/lei-si-san-shu-zhi-he-zai-wai-ceng-duo-yi-ci-xun-h/)
[wjq](https://leetcode-cn.com/problems/4sum/solution/kshu-zhi-he-by-kukubao207/)***
