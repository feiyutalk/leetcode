# 393. UTF-8 Validation

# Solution

这是位操作的题目，当然除了对位操作，还有就是要根据1的位数判断要进行多少次内层循环。这里求字节中前面有几个连续的1，我这里主要采用的是每次减掉2的k次幂，如果够减，就代表该位是1。

```java
class Solution {
    public boolean validUtf8(int[] data) {
        //boundary condition
        if(data == null || data.length < 1)
            return false;
        // case 1  0xxxx
        for(int i=0; i<data.length; i++){
            int oneBits  = getFirstOneBits(data[i]);
            if(oneBits == 1) return false;
            if(oneBits == 0) oneBits = 1;
            if(oneBits > 4) return false;
            for(int j=1; j<oneBits; j++){
                if(i+j >= data.length) return false;
                if(getFirstOneBits(data[i+j]) != 1) return false;
            }
            i = i+oneBits-1;
        }
        return true;
    }
    
    private int getFirstOneBits(int num){
        int mask = 0x000000FF;
        num = num & mask;
        int result = 0;
        int power = 7;
        while(num - Math.pow(2, power) >= 0){
            num -= Math.pow(2, power);
            power--;
            result++;
        }
        return result;
    }
}
```

