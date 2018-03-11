# 276. Paint Fence

## #1 动态规划[AC]

虽然题目是简单的，但是这种多状态空间的动态规划题目还是要留心，我们必须定义两个状态空间`int[] same`和`int[] diff`，其中，`same`记录的是当前位置和上一个位置一样时，总的可能数；`diff`记录的是当期值和上一个值不同时，总的可能数。

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

