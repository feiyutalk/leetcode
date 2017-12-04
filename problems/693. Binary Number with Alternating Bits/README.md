# 693. Binary Number with Alternating Bits

```java
class Solution {
    public boolean hasAlternatingBits(int n) {
        List<Integer> bits = new ArrayList<Integer>();
        while(n != 0){
            bits.add(n & 1);
            n /= 2;
        }
        for(int i=0; i<bits.size()-1; i++){
            if(bits.get(i) == bits.get(i+1))
                return false;
        }
        return true;
    }
}
```

