---
title: 149.直线上最多的点数（Max Points on a Line）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给定一个二维平面，平面上有 n 个点，求最多有多少个点在同一条直线上。

示例 1:
```
输入: [[1,1],[2,2],[3,3]]
输出: 3
解释:
^
|
|        o
|     o
|  o  
+------------->
0  1  2  3  4
```
示例 2:
```
输入: [[1,1],[3,2],[5,3],[4,1],[2,3],[1,4]]
输出: 4
解释:
^
|
|  o
|     o        o
|        o
|  o        o
+------------------->
0  1  2  3  4  5  6
```

# 题解

## 官方题解
暂无

## 其他题解
### 1.暴力法
**思路：**
三种判断点在直线的方法


```
public int maxPoints(int[][] points) {
    if (points.length < 3) {
        return points.length;
    }
    int i = 0;
    for (; i < points.length - 1; i++) {
        if (points[i][0] != points[i + 1][0] || points[i][1] != points[i + 1][1]) {
            break;
        }

    }
    if (i == points.length - 1) {
        return points.length;
    }
    int max = 0;
    for (i = 0; i < points.length; i++) {
        for (int j = i + 1; j < points.length; j++) {
            if (points[i][0] == points[j][0] && points[i][1] == points[j][1]) {
                continue;
            }
            int tempMax = 0;
            for (int k = 0; k < points.length; k++) {
                if (k != i && k != j) {
                    if (test(points[i][0], points[i][1], points[j][0], points[j][1], points[k][0], points[k][1])) {
                        tempMax++;
                    }
                }

            }
            if (tempMax > max) {
                max = tempMax;
            }
        }
    }
    //加上直线本身的两个点
    return max + 2;
}
/*private boolean test(int x1, int y1, int x2, int y2, int x, int y) {
	return (long)(y2 - y1) * (x - x2) == (long)(y - y2) * (x2 - x1);
}*/

/*private boolean test(int x1, int y1, int x2, int y2, int x, int y) {
    BigInteger x11 = BigInteger.valueOf(x1);
    BigInteger x22 = BigInteger.valueOf(x2);
    BigInteger y11 = BigInteger.valueOf(y1);
   	BigInteger y22 = BigInteger.valueOf(y2);
    BigInteger x0 = BigInteger.valueOf(x);
    BigInteger y0 = BigInteger.valueOf(y);
    return y22.subtract(y11).multiply(x0.subtract(x22)).equals(y0.subtract(y22).multiply(x22.subtract(x11)));
}*/

private boolean test(int x1, int y1, int x2, int y2, int x, int y) {
    int g1 = gcd(y2 - y1, x2 - x1);
    if(y == y2 && x == x2){
        return true;
    }
    int g2 = gcd(y - y2, x - x2);
    return (y2 - y1) / g1 == (y - y2) / g2 && (x2 - x1) / g1 == (x - x2) / g2;
}

private int gcd(int a, int b) {
    while (b != 0) {
        int temp = a % b;
        a = b;
        b = temp;
    }
    return a;
}

```

```
class Solution {
   int result = 0;

    public  int maxPoints(int[][] points) {
        int len = points.length;
        if (len < 3) {
            return len;
        }

        for (int i = 0; i < len - 1; i++) {
            int x = points[i + 1][0] - points[i][0];
            int y = points[i + 1][1] - points[i][1];
            if (x != 0 || y != 0) {
                maxPointsHelper(points, x, y, i);
            }
        }
        //怎么解决的重复点问题：
        //如果数组中所有点都相等，返回数组长度
        //只要有不相同的两个点，就能进入下面的方法，就能统计到所有的点
        return result == 0 ? len : result;
    }

    private  void maxPointsHelper(int[][] points, long a, long b, int base) {
        int path = 2;
        int len = points.length;
        for (int i = 0; i < len; i++) {
            if (i != base && i != base + 1) {
                if ((points[i][1] - points[base][1]) * a == (points[i][0] - points[base][0]) * b)
                {
                    path++;
                }
            }
        }
        result = Math.max(result, path);
    }
}
```

### 2.存入相同直线
**思路：**
对于 1,2，1,3 ，1,4 这些点求出来的表达式都是唯一确定的。

所以我们当考虑 1,2 两个点的时候，我们可以求出 k 和 b 把它存到 HashSet 中，然后当考虑 1,3 以及后边的点的时候，先求出 k 和 b，然后从 HashSet 中看是否存在即可。

当然存的时候，我们可以用一个技巧，key 存一个 String ，也就是 k + "@" + b 。



```
public int maxPoints(int[][] points) {
    if(points.length < 3){
        return points.length;
    }
    int i = 0;
    //判断所有点是否都相同的特殊情况
    for (; i < points.length - 1; i++) {
        if (points[i][0] != points[i + 1][0] || points[i][1] != points[i + 1][1]) {
            break;
        }

    }
    if (i == points.length - 1) {
        return points.length;
    }
    HashSet<String> set = new HashSet<>();
    int max = 0;
    for (i = 0; i < points.length; i++) {
        for (int j = i + 1; j < points.length; j++) {
            if (points[i][0] == points[j][0] && points[i][1] == points[j][1]) {
                continue;
            }
            String key = getK(points[i][0], points[i][1], points[j][0], points[j][1])
                       + "@"
                       + getB(points[i][0], points[i][1], points[j][0], points[j][1]);
            if (set.contains(key)) {
                continue;
            }
            int tempMax = 0;
            for (int k = 0; k < points.length; k++) {
                if (k != i && k != j) {
                    if (test(points[i][0], points[i][1], points[j][0], points[j][1], points[k][0], points[k][1])) {
                        tempMax++;
                    }
                }

            }
            if (tempMax > max) {
                max = tempMax;
            }
            set.add(key);
        }
    }
    return max + 2;
}

private double getB(int x1, int y1, int x2, int y2) {
    if (y2 == y1) {
        return Double.POSITIVE_INFINITY;
    }
    return (double) (x2 - x1) * (-y1) / (y2 - y1) + x1;
}

private double getK(int x1, int y1, int x2, int y2) {
    if (x2 - x1 == 0) {
        return Double.POSITIVE_INFINITY;
    }
    return (double) (y2 - y1) / (x2 - x1);
}

private boolean test(int x1, int y1, int x2, int y2, int x, int y) {
	return (long)(y2 - y1) * (x - x2) == (long)(y - y2) * (x2 - x1);
}

```

### 3.点斜式
**思路：**
![](https://pic.leetcode-cn.com/f9da822aada3c01a0eaf203d6df4107c58cf0cf06dc99082a32fa31360368c6d.jpg)

```
public int maxPoints(int[][] points) {
    if (points.length < 3) {
        return points.length;
    }
    int res = 0;
    //遍历每个点
    for (int i = 0; i < points.length; i++) {
        int duplicate = 0;
        int max = 0;//保存经过当前点的直线中，最多的点
        HashMap<String, Integer> map = new HashMap<>();
        for (int j = i + 1; j < points.length; j++) {
            //求出分子分母
            int x = points[j][0] - points[i][0];
            int y = points[j][1] - points[i][1];
            if (x == 0 && y == 0) {
                duplicate++;
                continue;

            }
            //进行约分
            int gcd = gcd(x, y);
            x = x / gcd;
            y = y / gcd;
            String key = x + "@" + y;
            map.put(key, map.getOrDefault(key, 0) + 1);
            max = Math.max(max, map.get(key));
        }
        //1 代表当前考虑的点，duplicate 代表和当前的点重复的点
        res = Math.max(res, max + duplicate + 1);
    }
    return res;
}

private int gcd(int a, int b) {
    while (b != 0) {
        int temp = a % b;
        a = b;
        b = temp;
    }
    return a;
}

```


---
***参考：
[LeetCode](https://leetcode-cn.com/problems/max-points-on-a-line/submissions/)
[windliang](https://leetcode-cn.com/problems/max-points-on-a-line/solution/xiang-xi-tong-su-de-si-lu-fen-xi-duo-jie-fa-by--35/)***
