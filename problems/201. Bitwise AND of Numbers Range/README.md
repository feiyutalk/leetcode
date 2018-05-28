# 201. Bitwise AND of Numbers Range

## #1 暴力搜索[TLE]

通过遍历区间`[m,n]`之间的所有数，然后依次相与，得到最后的结果。

```java
class Solution {
    public int rangeBitwiseAnd(int m, int n) {
        if(m > n)
            return -1;
        if(m == n)
            return m;
        int res = m;
        for(int i=m+1; i<=n; i++)
            res &= i;
        return res;
    }
}
```

- **时间复杂度**：$O(n-m)$
- **空间复杂度：**$O(1)$

## #2 位操作[AC]

该解法的想法如下：

1. `奇数 & 偶数`得到的结果的最后一位肯定是0；
2. 如果`m != n`，那`[m, n]`这个范围内肯定至少存在一个奇数和一个偶数，所以把该范围内的数相与后的结果的最后一位肯定是0;
3. 通过移位并不断重复上述的过程来求解最终结果不同位上的值。

```java
class Solution {
    public int rangeBitwiseAnd(int m, int n) {
        if(m > n)
            return -1;
        if(m == n)
            return m;
        int moveFactor = 1;
        while(m != n){
            m >>= 1;
            n >>= 1;
            moveFactor <<= 1;
        }
        return moveFactor*m; 
    }
}
```

