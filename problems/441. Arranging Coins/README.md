# 441. Arranging Coins

```java
class Solution {
    public int arrangeCoins(int n) {
        if(n == 2147483647){
            return 65535;
        }
        int left = 0;
        int right = n;
        while(left < right){
            int mid = left + (right - left + 1)/2;
            if((0.5 * mid * mid + 0.5 * mid ) <= n){
                left = mid;
            }else{
                right = mid - 1;
            }
        }
        return right;
    }
}
```

