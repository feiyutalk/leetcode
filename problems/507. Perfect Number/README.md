# 507. Perfect Number

```java
class Solution {
    public boolean checkPerfectNumber(int num) {
        if(num == 1) return false;
        int sum = 0;
        for(int i=2; i<=num/2; i++){
            if(num % i == 0){
                int j = num / i;
                if(j < i) break;
                sum += i;
                sum += j;
            }
        }
        return sum+1 == num;
    }
}
```

