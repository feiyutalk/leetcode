# 696. Count Binary Substrings

```java
class Solution {
    public int countBinarySubstrings(String s) {
        if(s == null || s.length() == 0)
            return 0;
        int[] group = new int[s.length()];
        group[0] = 1;
        int t = 0;
        for(int i=1; i<s.length(); i++){
            if(s.charAt(i) == s.charAt(i-1)){
                group[t]++;
            }else{
                group[++t] = 1;
            }
        }
        int res = 0;
        for(int i=1; i<group.length; i++){
            res += Math.min(group[i], group[i-1]);
        }
        return res;
    }
}
```

