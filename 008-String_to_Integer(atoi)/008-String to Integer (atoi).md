#  8. String to Integer (atoi)

## Description

```
Difficulty: Medium
Total Accepted:179.8K
Total Submissions:1.3M
Contributor: LeetCode
```

Implement atoi to convert a string to an integer.

**Hint:** Carefully consider all possible input cases. If you want a challenge, please do not see below and ask yourself what are the possible input cases.

**Notes: **It is intended for this problem to be specified vaguely (ie, no given input specs). You are responsible to gather all the input requirements up front.

**Requirements for atoi**:

The function first discards as many whitespace characters as necessary until the first non-whitespace character is found. Then, starting from this character, takes an optional initial plus or minus sign followed by as many numerical digits as possible, and interprets them as a numerical value.

The string can contain additional characters after those that form the integral number, which are ignored and have no effect on the behavior of this function.

If the first sequence of non-whitespace characters in str is not a valid integral number, or if no such sequence exists because either str is empty or it contains only whitespace characters, no conversion is performed.

If no valid conversion could be performed, a zero value is returned. If the correct value is out of the range of representable values, INT_MAX (2147483647) or INT_MIN (-2147483648) is returned.

***

## Solution1

  字符串转化为数值，这道题:sob:，边界条件真是。。。。。。啊。。。。。。花了我一个多小时，估计提交了20多次了。。。。本身题目不算难，就是遍历字符串中的每个字符，可以用charAt和计数器一起使用实现遍历字符串。关于正负号，可以先默认为正号，然后通过读取第一个字符是否为'+','-'来改变正负号，这里正负号可以用1或者-1来实现正负号，然后就是读取一个数字，然后乘以10，这样做了。还有，就是要考虑是否越界的问题，我在这里是遍历的过程中就判断，因为我之前试过了，在遍历完再判断，会出现input = 9223372036854775809; 也就是long的最大值也越了。。。尴尬:weary:.最后附上结果，应该还算可以吧:

![](/008-String_to_Integer(atoi)/StringToInteger.png)

```java
public class Solution {
    public int myAtoi(String str) {
        if(str == null){
            return 0;
        }
        str = str.trim();
        if(str.length() == 0){
            return 0;
        }

        int opt = 1; 
        int start = 1;
        long ans = 0l;
        
        opt = str.charAt(0);
        if(opt == '+'){
            opt = 1;
        }else if(opt == '-'){
            opt = -1;
        }else{
            opt = 1;
            start--;
        }
        int maxint = 0x7fffffff;
        int minint = 0x80000000;
        
        for(int i=start; i<str.length(); i++){
            if(!(str.charAt(start) >= '0' && str.charAt(start) <='9'))
                return 0;
            char tmp = str.charAt(i);
            if(tmp >= '0' && tmp <= '9'){
                ans = ans*10 + (tmp - '0');
                if(ans > maxint){
                    if(opt == -1)
                        return minint;
                    return maxint;
                 }
                 if(ans < minint){
                     if(opt == -1)
                        return maxint;
                    return minint;
                }
            }else{
                break;
            }
        }
        return (int)(opt * ans);
    }
}
```

***

**enjoy life, coding now! :D**
