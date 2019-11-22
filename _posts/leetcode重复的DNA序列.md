---
title: 187.重复的DNA序列（Repeated DNA Sequences）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [187\. 重复的DNA序列](https://leetcode-cn.com/problems/repeated-dna-sequences/)

Difficulty: **中等**


所有 DNA 都由一系列缩写为 A，C，G 和 T 的核苷酸组成，例如：“ACGAATTCCG”。在研究 DNA 时，识别 DNA 中的重复序列有时会对研究非常有帮助。

编写一个函数来查找 DNA 分子中所有出现超过一次的 10 个字母长的序列（子串）。

**示例：**

```
输入：s = "AAAAACCCCCAAAAACCCCCCAAAAAGGGTTT"
输出：["AAAAACCCCC", "CCCCCAAAAA"]
```


#### Solution1 - 滑动窗口

Language: **Java**

```java
class Solution {
    public List<String> findRepeatedDnaSequences(String s) {
        List<String> res=new ArrayList<>();
        //s长度小于等于10当然不会有重复子串
        if(s.length()<=10)
            return res;
        //窗口大小
        int window=10;
        int start=0;
        //记录出现过的子串
        Map<String,Integer> sMap=new HashMap<>();
            //左为0，右为窗口大小，开始滑动每轮while循环lr自增1
            int l=0;
            int r=window;
            while(r<=s.length()){
                //获取当前子串
                String temp=s.substring(l,r);
                //如果已经记录存在，返回对应value值，否则返回1
                int count=sMap.getOrDefault(temp,0);
                //value值加1，存入map
                sMap.put(temp,count+1);
                //第一次重复出现的时候加入list，之后再出现此单词不用加入list了，等于去重
                if(count==1){
                    res.add(temp);
                }
                l++;
                r++;
            }
        return res;
    }
}

​
```

#### Solution2 - 两个 set

Language: **Java**

```java
public List<String> findRepeatedDnaSequences(String s) {
    List<String> res = new ArrayList<>();
    if(s.length() < 10) return res;
    //储存已经遍历过的子字符串
    Set<String> set1 = new HashSet<>();
    //储存符合条件的子字符串
    Set<String> set2 = new HashSet<>();
    for(int i = 0;i + 10 <= s.length();i++){
        String seq = s.substring(i,i+10);
        if(set1.contains(seq)){
            set2.add(seq);
        }
        set1.add(seq);
    }
    res.addAll(set2);
    return res;
}

​
```
#### Solution3 - 位运算 + 数组标记

Language: **Java**

```java
class Solution {
 public List<String> findRepeatedDnaSequences(String s) {
        List<String> list = new ArrayList<String>();
        int[] num = new int[1 << 20];
        int k = (1 << 18) - 1, key = 0;
        for (int i = 0; i < s.length(); i++) {
            key <<= 2;
            key += getValue(s.charAt(i));
            if (i >= 9) {
                if (num[key] == 1) {
                    num[key]++;
                    list.add(s.substring(i - 9, i + 1));
                }
                else num[key]++;
                key &= k;
            }
        }
        return list;
    }


    private int getValue(char c) {
        switch (c) {
            case 'A':
                return 0;
            case 'C':
                return 1;
            case 'G':
                return 2;
            case 'T':
                return 3;
            default:
                throw new IllegalArgumentException("Illegal character");
        }
    }
}


​
```
```java
import java.util.List;
import java.util.HashMap;
import java.util.BitSet;

/**
    核心思想：hash
    1、hash表是一个bitmap
    2、以10个字符对应的数字和作为hash索引键
    3、bitmap中的每bit映射到一个10字符组成的字符串
*/
class Solution {
    public List<String> findRepeatedDnaSequences(String s) {
        List<String> list = new LinkedList<>();
        if(s == null || s.length() <= 10){
            return list;
        }

        // 将字符串映射成数字序列进行处理
        HashMap<Character, Integer> map = new HashMap<>();
        map.put('A', 0);
        map.put('C', 1);
        map.put('G', 2);
        map.put('T', 3);

        // 记录第一次出现的10字符子串
        BitSet bitSet = new BitSet(1 << 19);
        // 记录已经出现过两次或以上的10字符子串
        BitSet bitSetPre = new BitSet(1 << 19);

        int mask = 0b1111_1111_1111_1111_1111;
        int pos = 0;
        char[] charArray = s.toCharArray();

        // 先将最前面的10字符组成的子串记录在bitmap中
        for(int i = 0; i < 10; i++){
            pos = (pos << 2) | map.get(charArray[i]);
        }
        bitSet.set(pos);

        for(int i = 10; i < charArray.length; i++){
            // 移除最高位的字符，在末尾添加新的字符，是为字符串s的新10字符子串
            pos = (pos << 2) & mask | map.get(charArray[i]);

            // 该10字符组成的子串已被统计过
            if(bitSetPre.get(pos)){
                continue;
            }
            if(bitSet.get(pos)){
                // 10字符组成的子串第二次出现

                // 将当前10字符组成的子串添加到目标容器中
                list.add(s.substring(i - 9, i + 1));
                bitSetPre.set(pos);
            }else{

                // 10字符组成的子串第一次出现
                bitSet.set(pos);
            }
        }

        return list;
    }
}
```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/repeated-dna-sequences/submissions/)
[sxr](https://leetcode-cn.com/problems/repeated-dna-sequences/solution/chao-ji-jian-dan-si-lu-yi-kan-jiu-dong-hua-dong-ch/)
[mmmmmJCY](https://leetcode-cn.com/problems/repeated-dna-sequences/solution/java-shi-yong-liang-ge-set-by-zxy0917/)***
