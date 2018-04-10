# 190. Reverse Bits

## #1 位操作[AC]

算法步骤：

1. 每次从输入`n`中取最后一个数值，比如`n=00101`，则最后一个`1`被取出，具体做法是：

   ```java
   n & 1
   ```

2. 将`n`右移动一位，更新步骤1下一次的取值。

   ```java
   n >>>= 1; // >>>代表逻辑移位，即不考虑符号
   ```

3. 将步骤1得到的值加入到`result`结果中，并把`result`左移一位。

   ```java
   result += n & 1;
   result <<= 1;
   ```

```java
public class Solution {
    // you need treat n as an unsigned value
    public int reverseBits(int n) {
        int result = 0;
        for(int i=0; i<32; i++){
            result += n & 1;
            n >>>= 1;
            if(i < 31)
                result <<= 1;
        }
        return result;
    }
}
```

