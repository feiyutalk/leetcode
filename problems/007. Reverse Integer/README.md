# 7. Reverse Integer

## #1 依次取最低位[AC]
### 思路

这道题并不是很难，常见的利用去余和除的技巧去取得一个数的个位数。记得这道题在当年考研的时候刷机试题的时候就经常做，这道题的收获在于知道对于细节的处理，以及知道该怎么定义int的边界值，实际上用十六进制来表示更直观也更好记，然后就是要考虑取反后的溢出问题，这些细节以后要多注意。

### 算法

```java
public class Solution {
    public int reverse(int x) {
        long ans = 0l;
        int maxint = 0x7fffffff;
        int minint = 0x80000000;
        while(x != 0){
            ans = ans*10 + (x%10);
            x /= 10;
        }
        if(ans > maxint ||  ans < minint){
            return 0;
        }
        return (int)ans;
    }
}
```

### 复杂度分析：

- 时间复杂度：$O(32)$
- 空间复杂度：$O(1)$

