# 166. Fraction to Recurring Decimal
## Description

```
Difficulty: Easy
```

Given two integers representing the numerator and denominator of a fraction, return the fraction in string format.

If the fractional part is repeating, enclose the repeating part in parentheses.

For example,

- Given numerator = 1, denominator = 2, return "0.5".
- Given numerator = 2, denominator = 1, return "2".
- Given numerator = 2, denominator = 3, return "0.(6)".
## Solution 1
1. 在处理乘法除法的正负号的时候，可以用如下的技巧
	` (numerator>0)^(denominator>0)?"-":""`
2. 分类讨论的思路,在涉及到浮点数问题的时候，我们可以分整数，小数两部分来讨论。

```java

public class Solution {
    public String fractionToDecimal(int numerator, int denominator) {
        // 0? Max?
        if(numerator == 0)
            return "0";
        // 符号
        StringBuffer res = new StringBuffer();
        res.append((numerator>0)^(denominator>0)?"-":"");
        //越界
        long num = Math.abs((long)numerator);
        long den = Math.abs((long)denominator);
        
        //分类讨论 x<0 二次函数 x>0 ..
        //整数部分 和 小数部分
        // 整数部分
        res.append(num/den);
        //小数部分
        num %= den;
        if(num == 0)
            return res.toString();
        /*
        2 % 3 = 0.666
        整数  2/3 = 0
         res = 0.
        小数  2%3 = 2   
              2*10 / 3 = 6
              2 % 3 = 2 
              2 * 10 /3 = 6
              0.66666666
              0.333333
              0.21312443245543534532
        */
        res.append(".");
        Map<Long, Integer> map = new HashMap<Long, Integer>();
        map.put(num, res.length());
        while(num!=0){
            num *= 10;
            res.append(num/den);
            num %= den;
            if(map.containsKey(num)){
                int index = map.get(num);
                res.insert(index, "(");
                res.append(")");
                break;
            }else{
                map.put(num, res.length());
            }
        }
        return res.toString();
    }
}

```

***

**enjoy life, coding now! :D**
