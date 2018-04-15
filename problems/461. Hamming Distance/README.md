# 461. Hamming Distance

## #1 位操作[AC]

### 思路

通过异或这种操作可以得到这两个数哪些位置上数值不一样，然后在统计异或的结果中有几个1，就能得到海明距离。

### 算法

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

