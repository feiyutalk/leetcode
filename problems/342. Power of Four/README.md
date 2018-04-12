#  342. Power of Four

## #1 暴力搜索[TLE]

### 思路

依次搜索出所有的4的幂，如果与发现其中存在与输入值一样的，就返回true，否则就返回false。

### 算法

```java
class Solution {
    public boolean isPowerOfFour(int num) {
        if(num == 1)
            return true;
        if(num < 4)
            return false;
        int mul = 1;
        while(mul < num){
            mul *= 4;
            if(mul == num)
                return true;
        }
        return false;
    }
}
```

### 复杂度分析：

- 时间复杂度：$O(log_4num)$
- 空间复杂度：$O(1)$

## #2 位操作[AC]
### 思路

关于这道题目，前面有做过判断一个数是否为2的幂的问题，当时做的时候是把数值用二进制的域来看待，这样就可以发现，2的幂在2进制下的规律是，最高位为1，其他位为0，这道题要求4的幂。首先，4的幂是2的幂的一个子集，我们可以在之前题目的基础上，去思考这道题。复杂问题简单化思想，把该问题，转化为在求2的幂的解空间里求特定的子空间。第一步，先求出2的幂。第二步，在所有2的幂里面，找到4的幂。

对于第一步，我们通过`x&(x-1)==0`来过滤出2的幂，对于第二步呢？我们怎么判断，其实4的幂比2的幂多了一个限制条件，就是，它的1在奇数位上。所以，我们进一步用`0x55555555`过滤出4的幂。

### 算法

```java
public class Solution {
    public boolean isPowerOfFour(int num) {
        if(num <= 0)
            return false;
        return (((num&(num-1))==0)&&(num&0x55555555) != 0);
    }
}
```

### 复杂度分析

- 时间复杂度：$O(1)$
- 空间复杂度：$O(1)$

