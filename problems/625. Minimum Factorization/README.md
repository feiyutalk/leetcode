# 625. Minimum Factorization

```java
class Solution {
    public int smallestFactorization(int a) {
        //case 1, a < 10
        if(a < 10) return a;
        //case 2, a >= 10
        List<Integer> res = new ArrayList<>();
        for(int i=9; i>1; i--){
            while(a % i == 0){
                a /= i;
                res.add(i);
            }
        }
        if(a != 1) return 0;
        long mul = 0;
        for(int i=res.size()-1; i>=0; i--){
            mul = mul*10 + res.get(i);
        }
        if(mul > Integer.MAX_VALUE) return 0;
        return (int)mul;
    }
    
}
```

