# 125. Valid Palindrome
## Description

```
Difficulty: Easy
```
Given a string, determine if it is a palindrome, considering only alphanumeric characters and ignoring cases.

For example,

"A man, a plan, a canal: Panama" is a palindrome.

"race a car" is not a palindrome.

Note:

Have you consider that the string might be empty? This is a good question to ask during an interview.

For the purpose of this problem, we define empty string as valid palindrome.
## Solution 1
  这道题目的Note很关键，它给了我们一个提醒，这要让我们总结出写算法题的一些模式或者通用的步骤。我们可以在算法的第一步就去考虑异常的情况(特殊的输入)。所有，Note给的这个启发不旦旦是用在这道题目，对于所有的算法题，我们都可以这样来考虑。

  对于回文串的判断问题，我们可以通过定义头尾指针来判断，但是这道题目在进行判断的时候需要过滤掉不符合要求的字符，所以我们通过while循环来过滤掉不符合要求的字符。

```java

class Solution {
    public boolean isPalindrome(String s) {
        // I 
        if(s == null || s.length() == 0)
            return true;
        // II
        String ss = s.toLowerCase();
        for(int i=0,j=s.length()-1; i<j; i++, j--){
            while(i<j && !((isAlpha(ss.charAt(i)))||(isNumeric(ss.charAt(i)))))
                i++;
            while(i<j && !((isAlpha(ss.charAt(j)))||(isNumeric(ss.charAt(j)))))
                j--;
            if(ss.charAt(i) != ss.charAt(j))
                return false;
        }
        return true;
    }
    
    public boolean isAlpha(char c){
        return c >= 'a' && c <= 'z';
    }
    
    public boolean isNumeric(char c){
        return c >='0' && c <= '9';
    }
}
```

***

**enjoy life, coding now! :D**
