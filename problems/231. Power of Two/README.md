#  231. Power of Two

## #1 暴力搜索[AC]
 我的思路是如果这个数对2取余为1，就不是2的幂。依次类推，让这个数一直除以2，每一次都判断一下得到的数对2取余是否为1，如果是的话就返回false。提交后虽然AC了，但是结果不是很理想。。:sweat:

```java
public class Solution {
    public boolean isPowerOfTwo(int n) {
        if( n <= 0)
            return false;
        if(n == 1 || n == 2)
            return true;
        while(n > 1){
            if(n % 2 == 1)
                return false;
            n /= 2;
        }
        return true;
    }
}
```

## #2 暴力搜索[AC]

第二种搜索方式是，设置一个累积值，让该值不断的乘上2，并与输入进行比较，如果相同，则返回true；如果大于输入，则返回false。

```java
class Solution {
    public boolean isPowerOfTwo(int n) {
        if(n <= 0)
            return false;
        if(n == 1 || n == 2)
            return true;
        int max = n/2;
        long power = 2;
        for(int i=1; i<=max; i++){
            power *= 2;
            if(power > n)
                return false;
            if(power == n)
                return true;
        }
        return false;
    }
}
```

## #3 位操作[AC]

该解法用到了一个技巧和一个看待数值的角度，首先，看待2的幂之类的数值，尽量用2进制的角度去看， 这是一种经验，2的幂，在二进制的域里表现得及其有规律，而且和计算机运算结合非常紧密，我们结合这道题，看看换一种域看待数值，会有什么新的发现：

这里是二进制的世界：

| 数值   | 二进制表示 |
| ---- | ----- |
| 2    | 10    |
| 4    | 100   |
| 8    | 1000  |

从以上表格可以看出2的幂在二进制下的规律就是最高位为1，其他位为0，然后我们看一下把上面数值减去1得到的数值的二进制形式：

| 数值        | 二进制表示 |
| --------- | ----- |
| 2 - 1 = 1 | 01    |
| 4 - 1 = 3 | 011   |
| 8 - 1 = 7 | 0111  |

对比两个表，你是否发现一些规律呢？是的，我发现了，如果该值是2的幂，那么可以得到`n&(n-1) = 0`，那我们直接用这个技巧就可以判断了。

```java
public class Solution {
    public boolean isPowerOfTwo(int n) {
        if( n <= 0)
            return false;
        return (n&(n-1)) == 0;
    }
}
```




