# 14. Longest Common Prefix
## Description

```
Difficulty: Easy
```

Write a function to find the longest common prefix string amongst an array of strings.
## Solution 1
题目非常直观，只需要去遍历每个字符串中的每个字符即可，遇到不全一样的就退出。

```java

class Solution {
    public String longestCommonPrefix(String[] strs) {
        //boundary condition
        if(strs == null)
            return null;
        if(strs.length == 0)
            return "";
        
        //normal condition
        for(int i=0; ;i++){
            if(i == strs[0].length())
                return strs[0].substring(0, i);
            Character first = strs[0].charAt(i);
            for(String s : strs){
                if(i == s.length())
                    return strs[0].substring(0,i);
                if(s.charAt(i) != first)
                    return strs[0].substring(0, i);
            }
        }
    }
}
```

***

**enjoy life, coding now! :D**
