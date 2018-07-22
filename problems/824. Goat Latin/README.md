# 824. Goat Latin

## #1 规则编写[AC]

### 思路

1. 切分字符串成每个单词；
2. 对每个单词按照规则进行处理；

### 算法

```java
class Solution {
    public String toGoatLatin(String S) {
        if(S == null || S.length() == 0) return "";
        //split string
        String[] words = S.split(" ");
        //iterator every word, apply the rule
        StringBuilder res = new StringBuilder();
        for(int i=0; i<words.length; i++){
            String word = words[i];
            StringBuilder sb = new StringBuilder();
            //rule 1: begins with a, e, i, o, or u
            if(word.charAt(0) == 'a' || word.charAt(0) == 'e' || word.charAt(0) == 'i' || word.charAt(0) == 'o' || word.charAt(0) == 'u' || word.charAt(0) == 'A' || word.charAt(0) == 'E' || word.charAt(0) == 'I' || word.charAt(0) == 'O' || word.charAt(0) == 'U'){
                sb.append(word);
                sb.append("ma");
            }else{
                sb.append(word.substring(1));
                sb.append(word.substring(0,1));
                sb.append("ma");
            }
            for(int j=0; j<=i; j++)
                sb.append("a");
            res.append(sb.toString());
            if(i != words.length-1)
                res.append(" ");
        }
        return res.toString();
    }
}
```

### 复杂度分析

- 时间复杂度：$O(n^2)$

