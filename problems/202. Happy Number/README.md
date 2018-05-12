# 202. Happy Number

## #1 除于取余[AC]

### 算法

```java
class Solution {
    public boolean isHappy(int n) {
        Set<Integer> set = new HashSet<>();
        int remain = 0, sum = 0;
        while(set.add(n)){
            sum = 0;
            while(n > 0){
                remain = n % 10;
                sum += remain*remain;
                n /= 10;
            }
            if(sum == 1)
                return true;
            else
                n = sum;
        }
        return false;
    }
}
```

