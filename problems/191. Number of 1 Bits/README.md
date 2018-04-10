# 191. Number of 1 Bits

## #1 n&(n-1)[AC]
这道题才彻底把n&(n-1)这个二进制操作的技巧理解清楚，这个技巧的本质是消除最右边的那个1，利用这个技巧可以解决一系列的问题。比如数1问题，判断2的幂等。这是一类的题型，该类题型首先要抓住二进制特点，用二进制的角度看待数字，然后用该技巧去消除最右边的那个1，然后就能够得到我们想要的答案。

```java
public class Solution {
    // you need to treat n as an unsigned value
    public int hammingWeight(int n) {
        long sum = (long)n;
        if(sum < 0)
            sum += (0xffffffffl+1l);
        int count = 0;
        while(sum > 0){
            sum = sum&(sum-1);
            count++;
        }
        return count;
    }
}
```

## #2 计数[AC]
  我们还有其他的想法吗？关于数1的问题，可以把数值当做一串的0,1串，每次我们都对最后一个位进行判断，如果是1，则计数。然后右移一位，如此，直到为0为止。

```java
public class Solution {
    // you need to treat n as an unsigned value
    public int hammingWeight(int n) {
        int count = 0;
        while(n != 0){
            count = count + (n&1);
            n = n >>> 1;
        }
        return count;
    }
}
```


