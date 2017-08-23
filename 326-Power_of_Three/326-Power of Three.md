# 326. Power of Three

## Description

```
Difficulty: Easy
Total Accepted:98.9K
Total Submissions:246K
Contributor: LeetCode
```

Given an integer, write a function to determine if it is a power of three.

## Solution1
今天做多了，，，最后一道题用比较笨的方法把。。。

```java
public class Solution {
    public boolean isPowerOfThree(int n) {
        if(n <= 0)
            return false;
        if(n == 1)
            return true;
        while(n != 1){
            if(n%3 != 0)
                return false;
            n/=3;
        }
        return true;
    }
}
```

***

**enjoy life, coding now! :D**