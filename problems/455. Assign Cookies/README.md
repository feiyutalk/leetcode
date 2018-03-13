# 455. Assign Cookies

## #1 贪心[AC]

```java
class Solution {
    public int findContentChildren(int[] g, int[] s) {
        if(g == null || g.length == 0 || s == null || s.length == 0)
            return 0;
        Arrays.sort(g);
        Arrays.sort(s);
        int child = 0;
        int index = 0;
        while(child < g.length && index < s.length){
            if(g[child] <= s[index]){
                // current cookies satisfy content
                child++;
                index++;
            }else{
                // current cookies not satisfy content
                index++;
            }
        }
        return child;
    }
}
```

