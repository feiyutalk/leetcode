# 276. Paint Fence

```java
class Solution {
    public int numWays(int n, int k) {
        if(n == 0) return 0;
        if(n == 1) return k;
        int same = 0, diff = k, total = k;
        for(int i=2; i<=n; i++){
            same = diff;
            diff = (k-1)*total;
            total = same + diff;
        }
        return total;
    }
}
```

