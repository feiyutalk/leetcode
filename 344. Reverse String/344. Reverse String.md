# 344. Reverse String
## Description

```
Difficulty: Easy
```

Write a function that takes a string as input and returns the string reversed.

Example:

Given s = "hello", return "olleh".
## Solution 1
 
```java

public class Solution {
    public String reverseString(String s) {
        char[] chars = s.toCharArray();
        for(int left = 0, right = chars.length-1; left < right; left++, right--){
            char temp = chars[left];
            chars[left] = chars[right];
            chars[right] = temp;
        }
        return new String(chars);
    }
}
```

***

**enjoy life, coding now! :D**
