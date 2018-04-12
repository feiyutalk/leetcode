# 320. Generalized Abbreviation

## #1 递归枚举[AC]
### 思路

任何一个单词，有多少种abbreviation呢？答案是$2^n$种，因为对于单词里的每个字符，我们都有两种选择， 替换或者不替换该字符，如果选择替换该字符，那么就将计数器+1，并且当前的暂存字符串保持不变；如果不替换该字符，那么就将之前计数器的值以及该字符加入到暂存字符中，并重置计数器。

### 算法

```java
class Solution {
    public List<String> generateAbbreviations(String word) {
        if(word == null || word.length() == 0)
            return new ArrayList<String>(Arrays.asList(new String[]{""}));
        List<String> res = new ArrayList<>();
        helper(res, word, 0, "", 0);
        return res;
    }
    
    public void helper(List<String> res, String word, int pos, String cur, int count){
        if(pos == word.length()){
            if(count > 0)
                cur += count;
            res.add(cur);
        }else{
            //case1 保留当前字符
            helper(res, word, pos+1, cur + (count > 0 ? count : "") + word.charAt(pos), 0);
            //case2 替换当前字符
            helper(res, word, pos+1, cur, count+1);
        }
    }
}
```

### 复杂度分析

- 时间复杂度：$O(n\cdot 2^n)$
- 空间复杂度：$O(n)$

## #2 bitmap位图[AC]
### 思路

从上面的分析可以看出，其实上每一种abbreviation都对应单词中，一些字符被替换，一些字符不被替换，如果我们用1表示被替换，0表示不被替换，那么每一种abbreviation后的单词都对应着一个唯一的0/1串，我们可以遍历所有的0/1串，再利用这些0/1串来生成最后的字符串。

### 算法

```java
class Solution {
    public List<String> generateAbbreviations(String word) {
        if(word == null || word.length() == 0)
            return new ArrayList<String>(Arrays.asList(new String[]{""}));
        List<String> res = new ArrayList<>();
        for(int x=0; x < (1<<word.length()); x++)
            res.add(abbr(word, x));
        return res;
    }
    
    public String abbr(String word, int x){
        StringBuffer sb = new StringBuffer();
        int k = 0;
        for(int i=0; i<word.length(); x>>=1, i++){
            if((x & 1) == 0){// current bit is 0
                if(k != 0){
                    sb.append(k);
                }
                sb.append(word.charAt(i));
                k = 0;
            }else{// current bit is 1
                k++;
            }
        }
        if(k != 0)
            sb.append(k);
        return sb.toString();
    }
}
```

### 复杂度分析

- 时间复杂度：$O(n\cdot 2^n)$
- 空间复杂度：$