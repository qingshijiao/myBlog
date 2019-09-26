---
title: 65. 有效数字（Valid Number）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
验证给定的字符串是否可以解释为十进制数字。

例如:
```
"0" => true
" 0.1 " => true
"abc" => false
"1 a" => false
"2e10" => true
" -90e3   " => true
" 1e" => false
"e3" => false
" 6e-1" => true
" 99e2.5 " => false
"53.5e93" => true
" --6 " => false
"-+3" => false
"95a54e53" => false
```

**说明:** 我们有意将问题陈述地比较模糊。在实现代码之前，你应当事先思考所有可能的情况。这里给出一份可能存在于有效十进制数字中的字符列表：

- 数字 0-9
- 指数 - "e"
- 正/负号 - "+"/"-"
- 小数点 - "."

当然，在输入中，这些字符的上下文也很重要。



# 题解

## 官方题解
暂无

## 其他题解
### 1.直接条件判断
**思路：**
```
public boolean isNumber(String s) {
    s = s.trim();

    boolean pointSeen = false;
    boolean eSeen = false;
    boolean numberSeen = false;
    boolean numberAfterE = true;
    for(int i=0; i<s.length(); i++) {
        if('0' <= s.charAt(i) && s.charAt(i) <= '9') {
            numberSeen = true;
            numberAfterE = true;
        } else if(s.charAt(i) == '.') {
            if(eSeen || pointSeen) {
                return false;
            }
            pointSeen = true;
        } else if(s.charAt(i) == 'e') {
            if(eSeen || !numberSeen) {
                return false;
            }
            numberAfterE = false;
            eSeen = true;
        } else if(s.charAt(i) == '-' || s.charAt(i) == '+') {
            if(i != 0 && s.charAt(i-1) != 'e') {
                return false;
            }
        } else {
            return false;
        }
    }

    return numberSeen && numberAfterE;
}
```
**复杂度分析：**
- 时间复杂度：O(n)。
- 空间复杂度：O(1)。


### 2.正则表达式
**思路：**
使用正则式匹配（暂时由问题，不知道为什么能匹配“0e”）

```
import java.util.regex.*;
class Solution {
    public boolean isNumber(String s) {
        s = s.trim();
        Pattern p = Pattern.compile("^[\\+\\-]?(\\d+)|(\\d+\\.)|(\\d+\\.\\d+)|(\\.\\d+)(e[\\+\\-]?\\d+)?$");
        Matcher m = p.matcher(s);
       if (m.find()){
            return true;
        }
        return false;
    }

}
```
**复杂度分析：**
- 时间复杂度：O(n)。
- 空间复杂度：O(1)。


### 3.自动机
**思路：**
类似对每个字符进行判断，合法的状态由四个输出口
![](https://pic.leetcode-cn.com/76e2e607a9a9ea2f10b21da715ac09ea7a3c7ca6a571e75b0fab71deb204bef4-image.png)

```
class Solution {
  public boolean isNumber(String s) {
    int state = 0;
    s = s.trim();//去除头尾的空格
    //遍历所有字符，当做输入
    for (int i = 0; i < s.length(); i++) {
        switch (s.charAt(i)) {
             //输入正负号
            case '+':
            case '-':
                if (state == 0) {
                    state = 1;
                } else if (state == 4) {
                    state = 6;
                } else {
                    return false;
                }
                break;
            //输入数字
            case '0':
            case '1':
            case '2':
            case '3':
            case '4':
            case '5':
            case '6':
            case '7':
            case '8':
            case '9':
                //根据当前状态去跳转
                switch (state) {
                    case 0:
                    case 1:
                    case 2:
                        state = 2;
                        break;
                    case 3:
                        state = 3;
                        break;
                    case 4:
                    case 5:
                    case 6:
                        state = 5;
                        break;
                    case 7:
                        state = 8;
                        break;
                    case 8:
                        state = 8;
                        break;
                    default:
                        return false;
                }
                break;
            //小数点
            case '.':
                switch (state) {
                    case 0:
                    case 1:
                        state = 7;
                        break;
                    case 2:
                        state = 3;
                        break;
                    default:
                        return false;
                }
                break;
            //e
            case 'e':
                switch (state) {
                    case 2:
                    case 3:
                    case 8:
                        state = 4;
                        break;
                    default:
                        return false;
                }
                break;
            default:
                return false;

        }
    }
    //橙色部分的状态代表合法数字
    return state == 2 || state == 3 || state == 5 || state == 8;
  }


}
```

### 4.有限状态机
**思路：**
构建出来的状态机如封面图片所示（红色为 终止状态，蓝色为 中间状态）。根据《编译原理》的解释，DFA 从状态 0 接受串 s 作为输入。当s耗尽的时候如果当前状态处于中间状态，则拒绝；如果到达终止状态，则接受。

然后，根据 DFA 列出如下的状态跳转表，之后我们就可以采用 表驱动法 进行编程实现了。需要注意的是，这里面多了一个状态 8，是用于处理串后面的若干个多余空格的。所以，所有的终止态都要跟上一个状态 8。其中，有一些状态标识为-1，是表示遇到了一些意外的字符，可以直接停止后续的计算。状态跳转表如下：

![](https://pic.leetcode-cn.com/0683d701f2948a2bd8c235867c21a3aed5977691f129ecf34d681d43d57e339c-DFA.jpg)

![](https://i.loli.net/2019/09/26/ySi8TU3jtCWxpNa.png)

```
class Solution {
    public int make(char c) {
        switch(c) {
            case ' ': return 0;
            case '+':
            case '-': return 1;
            case '.': return 3;
            case 'e': return 4;
            default:
                if(c >= 48 && c <= 57) return 2;
        }
        return -1;
    }

    public boolean isNumber(String s) {
        int state = 0;
        int finals = 0b101101000;
        int[][] transfer = new int[][]{{ 0, 1, 6, 2,-1},
                                       {-1,-1, 6, 2,-1},
                                       {-1,-1, 3,-1,-1},
                                       { 8,-1, 3,-1, 4},
                                       {-1, 7, 5,-1,-1},
                                       { 8,-1, 5,-1,-1},
                                       { 8,-1, 6, 3, 4},
                                       {-1,-1, 5,-1,-1},
                                       { 8,-1,-1,-1,-1}};
        char[] ss = s.toCharArray();
        for(int i=0; i < ss.length; ++i) {
            int id = make(ss[i]);
            if (id < 0) return false;
            state = transfer[state][id];
            if (state < 0) return false;
        }
        return (finals & (1 << state)) > 0;
    }
}

```




### 5.责任链模式
**思路：** 利用接口和抽象类，为字符串进行是否为整数、小数、科学计数等判断。

```
interface NumberValidate {

	boolean validate(String s);
}

abstract class  NumberValidateTemplate implements NumberValidate{

public boolean validate(String s)
	{
		if (checkStringEmpty(s))
		{
			return false;
		}

		s = checkAndProcessHeader(s);

		if (s.length() == 0)
		{
			return false;
		}

		return doValidate(s);
	}

	private boolean checkStringEmpty(String s)
	{
		if (s.equals(""))
		{
			return true;
		}

		return false;
	}

	private String checkAndProcessHeader(String value)
	{
	    value = value.trim();

		if (value.startsWith("+") || value.startsWith("-"))
		{
			value = value.substring(1);
		}


		return value;
	}



	protected abstract boolean doValidate(String s);
}

class NumberValidator implements NumberValidate {

	private ArrayList<NumberValidate> validators = new ArrayList<NumberValidate>();

	public NumberValidator()
	{
		addValidators();
	}

	private  void addValidators()
	{
		NumberValidate nv = new IntegerValidate();
		validators.add(nv);

		nv = new FloatValidate();
		validators.add(nv);

		nv = new HexValidate();
		validators.add(nv);

		nv = new SienceFormatValidate();
		validators.add(nv);
	}

	@Override
	public boolean validate(String s)
	{
		for (NumberValidate nv : validators)
		{
			if (nv.validate(s) == true)
			{
				return true;
			}
		}

		return false;
	}


}

class IntegerValidate extends NumberValidateTemplate{

	protected boolean doValidate(String integer)
	{
		for (int i = 0; i < integer.length(); i++)
		{
			if(Character.isDigit(integer.charAt(i)) == false)
			{
				return false;
			}
		}

		return true;
	}
}

class HexValidate extends NumberValidateTemplate{

	private char[] valids = new char[] {'a', 'b', 'c', 'd', 'e', 'f'};
	protected boolean doValidate(String hex)
	{
		hex = hex.toLowerCase();
		if (hex.startsWith("0x"))
		{
			hex = hex.substring(2);
		}
		else
		{
		    return false;
		}

		for (int i = 0; i < hex.length(); i++)
		{
			if (Character.isDigit(hex.charAt(i)) != true && isValidChar(hex.charAt(i)) != true)
			{
				return false;
			}
		}

		return true;
	}

	private boolean isValidChar(char c)
	{
		for (int i = 0; i < valids.length; i++)
		{
			if (c == valids[i])
			{
				return true;
			}
		}

		return false;
	}
}

class SienceFormatValidate extends NumberValidateTemplate{

protected boolean doValidate(String s)
	{
		s = s.toLowerCase();
		int pos = s.indexOf("e");
		if (pos == -1)
		{
			return false;
		}

		if (s.length() == 1)
		{
			return false;
		}

		String first = s.substring(0, pos);
		String second = s.substring(pos+1, s.length());

		if (validatePartBeforeE(first) == false || validatePartAfterE(second) == false)
		{
			return false;
		}


		return true;
	}

	private boolean validatePartBeforeE(String first)
	{
		if (first.equals("") == true)
		{
			return false;
		}

		if (checkHeadAndEndForSpace(first) == false)
		{
			return false;
		}

		NumberValidate integerValidate = new IntegerValidate();
		NumberValidate floatValidate = new FloatValidate();
		if (integerValidate.validate(first) == false && floatValidate.validate(first) == false)
		{
			return false;
		}

		return true;
	}

private boolean checkHeadAndEndForSpace(String part)
	{

		if (part.startsWith(" ") ||
				part.endsWith(" "))
		{
			return false;
		}

		return true;
	}

	private boolean validatePartAfterE(String second)
	{
		if (second.equals("") == true)
		{
			return false;
		}

		if (checkHeadAndEndForSpace(second) == false)
		{
			return false;
		}

		NumberValidate integerValidate = new IntegerValidate();
		if (integerValidate.validate(second) == false)
		{
			return false;
		}

		return true;
	}
}

class FloatValidate extends NumberValidateTemplate{

   protected boolean doValidate(String floatVal)
	{
		int pos = floatVal.indexOf(".");
		if (pos == -1)
		{
			return false;
		}

		if (floatVal.length() == 1)
		{
			return false;
		}

		NumberValidate nv = new IntegerValidate();
		String first = floatVal.substring(0, pos);
		String second = floatVal.substring(pos + 1, floatVal.length());

		if (checkFirstPart(first) == true && checkFirstPart(second) == true)
		{
			return true;
		}

		return false;
	}

	private boolean checkFirstPart(String first)
	{
	    if (first.equals("") == false && checkPart(first) == false)
	    {
	    	return false;
	    }

	    return true;
	}

	private boolean checkPart(String part)
	{
	   if (Character.isDigit(part.charAt(0)) == false ||
				Character.isDigit(part.charAt(part.length() - 1)) == false)
		{
			return false;
		}

		NumberValidate nv = new IntegerValidate();
		if (nv.validate(part) == false)
		{
			return false;
		}

		return true;
	}
}

class Solution {
    public boolean isNumber(String s) {
        NumberValidate nv = new NumberValidator();

	    return nv.validate(s);
    }
}
```


---
***参考：
[LeetCode](https://leetcode-cn.com/problems/valid-number/)
[Una_zh](https://leetcode-cn.com/problems/valid-number/solution/yong-zheng-ze-biao-da-shi-jie-jue-you-xiao-shu-zi-/)
[windliang](https://leetcode-cn.com/problems/valid-number/solution/xiang-xi-tong-su-de-si-lu-fen-xi-duo-jie-fa-by-1-4/)
[user8973](https://leetcode-cn.com/problems/valid-number/solution/biao-qu-dong-fa-by-user8973/)***
