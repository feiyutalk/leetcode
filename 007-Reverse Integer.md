#Description

:star2:star2:

Reverse digits of an integer.

Example1: x = 123, return 321

Example2: x = -123, return -321

***
##Analysis
这道题并不是很难，常见的利用去余和除的技巧去取得一个数的个位数。记得这道题在当年考研的时候刷机试题的时候就经常做，这道题的收获在于知道对于细节的处理，以及知道该怎么定义int的边界值，实际上用十六进制来表示更直观也更好记，然后就是要考虑去反后的溢出问题，这些细节以后要多注意。

##Solution

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

***
enjoy life, coding now! :D 