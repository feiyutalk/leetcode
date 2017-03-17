# Description
:star2:

Given a non-negative integer num, repeatedly add all its digits until the result has only one digit.

For example:

Given num = 38, the process is like: 3 + 8 = 11, 1 + 1 = 2. Since 2 has only one digit, return it.

Follow up:

Could you do it without any loop/recursion in O(1) runtime?

## Analysis
这道题目本身不难，但是采用传统的方式做，取出各位然后相加，如果大于10，继续，这样的循环方式，还是有点繁琐，我们可以采用如下代码中的技巧来算：

## Solution
```java
public class Solution {
    public int addDigits(int num) {
        return ((num-1)%9 +1);
    }
}
```

***
enjoy life, coding now!:D