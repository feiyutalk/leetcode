# 686. Repeated String Match

## #1 暴力搜索[TLE]

### 思路

遍历所有可能的字符串，然后对每个可能的字符串进行判断，判断字符串`B`是否是该字符串的子串。

### 算法

```java
class Solution {
    public int repeatedStringMatch(String A, String B) {
        if(A == null || A.length() == 0) return B==null||B.length() == 0?1:-1;
        int count=1;
        StringBuilder sb = new StringBuilder(A);
        while(sb.length() < B.length()){
            sb.append(A);
            count++;
        }
        for(int i=0; i<count; i++){
            if(isSubstring(sb.toString(), B))
                return count;
            sb.append(A);
            count++;
        }
        return -1;
    }
    
    public boolean isSubstring(String A, String B){
        // A: abcd
        // B: bcdab
        for(int i=0; i<=A.length()-B.length(); i++){
            int k=i;
            int j=0;
            while(j < B.length() && B.charAt(j) == A.charAt(k)){
                j++;
                k++;
            }
            if(j == B.length())
                return true;
        }
        return false;
    }
}
```

### 复杂度分析

- 时间复杂度：$O(k\cdot 2n)$

