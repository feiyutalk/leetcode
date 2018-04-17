# 50. Pow(x, n)

## #1 取幂[AC]

### 思路

### 算法

```java
class Solution {
    public double myPow(double x, int n) {
        long ln = n;
        if(n == 0) return 1;
        if(ln < 0){
            x = 1/x;
            ln = -ln;
        }
        double res = 1;
        while(ln > 0){
            if((ln & 1) == 1){
                res *= x;
            }
            x *= x;
            ln >>= 1;
        }
        return res;
    }
}
```

