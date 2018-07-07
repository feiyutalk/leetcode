# 408. Valid Word Abbreviation

## #1 遍历解析法[AC]

### 思路

我们通过设置两个指针`i,j`，分别遍历字符串`word`和`abbr`，如果当前字符串是一样的，就继续，如果不一样，就解析`j`指针所指向的数字，然后让`i`指针向后移动`n`位。

### 算法

```java
class Solution {
    public boolean validWordAbbreviation(String word, String abbr) {
        if(word == null || word.length() == 0) return false;
        if(abbr == null || abbr.length() == 0) return false;
        int j=0;
        int i=0;
        for(; i<word.length() && j < abbr.length(); i++, j++){
            if(word.charAt(i) == abbr.charAt(j))
                continue;
            else{
                if(abbr.charAt(j) == '0')
                    return false;
                int num = abbr.charAt(j) - '0';
                while(j+1 < abbr.length() && Character.isDigit(abbr.charAt(j+1))){
                    num = num * 10 + abbr.charAt(j+1) - '0';
                    j++;
                }
                i = i + num - 1;
            }
        }
        return i == word.length() && j == abbr.length();
    }
}
```

### 复杂度分析

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$