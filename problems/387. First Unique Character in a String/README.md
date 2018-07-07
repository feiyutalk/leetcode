# 387. First Unique Character in a String

## #1 过滤出重复元素[AC]

### 思路

通过`set`来记录已经访问过的元素，依次遍历字符串中的每个字符，如果该字符之前已经访问过了，那么就把它加到一个`list`中，最后，从左往右遍历，找出第一个没在`list`中出现的元素，返回其下标。

### 算法

```java
class Solution {
    public int firstUniqChar(String s) {
        if(s == null || s.length() == 0) return -1;
        Set<Character> set = new HashSet<>();
        List<Character> dup = new ArrayList<>();
        for(Character c : s.toCharArray()){
            if(set.contains(c))
                dup.add(c);
            else
                set.add(c);
        }
        for(int i=0; i<s.length(); i++){
            if(!dup.contains(s.charAt(i)))
                return i;
        }
        return -1;
    }
}
```

### 复杂度分析

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$

