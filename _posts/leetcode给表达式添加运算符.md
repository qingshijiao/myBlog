---
title: 282.给表达式添加运算符 (Expression Add Operators)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [282\. 给表达式添加运算符](https://leetcode-cn.com/problems/expression-add-operators/)

Difficulty: **困难**


给定一个仅包含数字 `0-9` 的字符串和一个目标值，在数字之间添加**二元**运算符（不是一元）`+`、`-` 或 `*` ，返回所有能够得到目标值的表达式。

**示例 1:**

```
输入: num = "123", target = 6
输出: ["1+2+3", "1*2*3"]
```

**示例 2:**

```
输入: num = "232", target = 8
输出: ["2*3+2", "2+3*2"]
```

**示例 3:**

```
输入: num = "105", target = 5
输出: ["1*0+5","10-5"]
```

**示例 4:**

```
输入: num = "00", target = 0
输出: ["0+0", "0-0", "0*0"]
```

**示例 5:**

```
输入: num = "3456237490", target = 9191
输出: []
```


#### Solution - 回溯

Language: **Java**

```java
​class Solution {

  public ArrayList<String> answer;
  public String digits;
  public long target;

  public void recurse(
      int index, long previousOperand, long currentOperand, long value, ArrayList<String> ops) {
    String nums = this.digits;

    // Done processing all the digits in num
    if (index == nums.length()) {

      // If the final value == target expected AND
      // no operand is left unprocessed
      if (value == this.target && currentOperand == 0) {
        StringBuilder sb = new StringBuilder();
        ops.subList(1, ops.size()).forEach(v -> sb.append(v));
        this.answer.add(sb.toString());
      }
      return;
    }

    // Extending the current operand by one digit
    currentOperand = currentOperand * 10 + Character.getNumericValue(nums.charAt(index));
    String current_val_rep = Long.toString(currentOperand);
    int length = nums.length();

    // To avoid cases where we have 1 + 05 or 1 * 05 since 05 won't be a
    // valid operand. Hence this check
    if (currentOperand > 0) {

      // NO OP recursion
      recurse(index + 1, previousOperand, currentOperand, value, ops);
    }

    // ADDITION
    ops.add("+");
    ops.add(current_val_rep);
    recurse(index + 1, currentOperand, 0, value + currentOperand, ops);
    ops.remove(ops.size() - 1);
    ops.remove(ops.size() - 1);

    if (ops.size() > 0) {

      // SUBTRACTION
      ops.add("-");
      ops.add(current_val_rep);
      recurse(index + 1, -currentOperand, 0, value - currentOperand, ops);
      ops.remove(ops.size() - 1);
      ops.remove(ops.size() - 1);

      // MULTIPLICATION
      ops.add("*");
      ops.add(current_val_rep);
      recurse(
          index + 1,
          currentOperand * previousOperand,
          0,
          value - previousOperand + (currentOperand * previousOperand),
          ops);
      ops.remove(ops.size() - 1);
      ops.remove(ops.size() - 1);
    }
  }

  public List<String> addOperators(String num, int target) {

    if (num.length() == 0) {
      return new ArrayList<String>();
    }

    this.target = target;
    this.digits = num;
    this.answer = new ArrayList<String>();
    this.recurse(0, 0, 0, 0, new ArrayList<String>());
    return this.answer;
  }
}

```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/expression-add-operators/solution/gei-biao-da-shi-tian-jia-yun-suan-fu-by-leetcode/)***
