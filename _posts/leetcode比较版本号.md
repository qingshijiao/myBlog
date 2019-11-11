---
title: 165.比较版本号（Compare Version Numbers）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
比较两个版本号 version1 和 version2。
如果 version1 > version2 返回 1，如果 version1 < version2 返回 -1， 除此之外返回 0。

你可以假设版本字符串非空，并且只包含数字和 . 字符。

 . 字符不代表小数点，而是用于分隔数字序列。

例如，2.5 不是“两个半”，也不是“差一半到三”，而是第二版中的第五个小版本。

你可以假设版本号的每一级的默认修订版号为 0。例如，版本号 3.4 的第一级（大版本）和第二级（小版本）修订号分别为 3 和 4。其第三级和第四级修订号均为 0。
 

示例 1:
```
输入: version1 = "0.1", version2 = "1.1"
输出: -1
```
示例 2:
```
输入: version1 = "1.0.1", version2 = "1"
输出: 1
```
示例 3:
```
输入: version1 = "7.5.2.4", version2 = "7.5.3"
输出: -1
```
示例 4：
```
输入：version1 = "1.01", version2 = "1.001"
输出：0
解释：忽略前导零，“01” 和 “001” 表示相同的数字 “1”。
```
示例 5：
```
输入：version1 = "1.0", version2 = "1.0.0"
输出：0
解释：version1 没有第三级修订号，这意味着它的第三级修订号默认为 “0”。
 ```

**提示：**

版本字符串由以点 （.） 分隔的数字字符串组成。这个数字字符串可能有前导零。
版本字符串不以点开始或结束，并且其中不会有两个连续的点。


# 题解

## 官方题解
暂无

## 其他题解
### 1.字符串切分
**思路：** 字符串按'.'分割
```
class Solution {
    public int compareVersion(String version1, String version2) {
        String[] v1 = version1.split("\\.");//得到两个版本号分别对应的字符串数组v1和v2
        String[] v2 = version2.split("\\.");
        for (int i = 0, j = 0; i < v1.length || j < v2.length; i++, j++) {
            int n1 = i < v1.length ? Integer.parseInt(v1[i]) : 0;
            int n2 = j < v2.length ? Integer.parseInt(v2[j]) : 0;//如果i、j大于v1、v2的length，取0；
                                        //否则用Integer.parseInt()来转换，像“001”这种会自动转换为1
            if (n1 == n2) {
                continue;//如果n1和n2相等，继续循环
            } else {
                return n1 > n2 ? 1 : -1;//如果n1大，说明第一个版本大，返回1；否则返回-1
            }
        }
        return 0;//如果循环结束都没有返回结果，说明版本是一样的，返回0
    }
}
```

### 2.逐一比较
**思路：**
```
class Solution {
    public int compareVersion(String version1, String version2) {
        //循环读取每一个版本字符串的最近一个.前的数字并计算其值
        int len1=version1.length();
        int len2=version2.length();
        for(int i=0,j=0;i<len1||j<len2;){
            int num1=0;
            int num2=0;
            while(i<len1&&version1.charAt(i)!='.'){
                num1=num1*10+(version1.charAt(i)-'0');
                i++;
            }
            while(j<len2&&version2.charAt(j)!='.'){
                num2=num2*10+(version2.charAt(j)-'0');
                j++;
            }
            //比较两个值的大小，若相同则继续比较
            if(num1>num2){
                return 1;
            }else if(num1<num2){
                return -1;
            }else{
                i++;
                j++;
            }
        }

        return 0;
    }
}
```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/compare-version-numbers/submissions/)
[fatwxy](https://leetcode-cn.com/problems/compare-version-numbers/solution/jiang-ban-ben-hao-zhuan-huan-wei-yong-yi-ge-dian-g/)***
