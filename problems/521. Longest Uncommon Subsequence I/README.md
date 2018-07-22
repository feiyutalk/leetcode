# 521. Longest Uncommon Subsequence I

## #1 暴力搜索[TLE]

### 思路

用深度搜索的方式遍历所有的可能的子序列，然后在这些搜索的子序列里面找出只出现过一次的最大子序列。为了统计哪些子序列只出现1次，我们可以使用`HashMap`来记录每个字序列出现的次数。

### 算法

```java
class Solution {
    Map<String, Integer> res = new HashMap<>();
    public int findLUSlength(String a, String b) {
        if(a == null || a.length() == 0) return b==null||b.length()==0?-1:b.length();
        if(b == null || b.length() == 0) return a==null||a.length()==0?-1:a.length();
        dfs(a.toCharArray(), 0, new StringBuilder());
        dfs(b.toCharArray(), 0, new StringBuilder());
        int max = -1;
        for(Map.Entry<String, Integer> entry : res.entrySet()){
            if(entry.getValue() == 1)
                max = Math.max(max, entry.getKey().length());
        }
        return max;
    }
    
    public void dfs(char[] chars, int step, StringBuilder sb){
        if(step == chars.length){
            res.put(sb.toString(), res.getOrDefault(sb.toString(), 0) + 1);
            return;
        }
        //要该字符
        sb.append(chars[step]);
        dfs(chars, step+1, sb);
        //不要该字符
        sb.setLength(sb.length()-1);
        dfs(chars, step+1, sb);
    }
}
```

### 复杂度分析

- 时间复杂度：$O(2^n)$

