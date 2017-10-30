# 660. Remove 9

Description
-----------

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Difficulty: Hard
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Start from integer 1, remove any integer that contains 9 such as 9, 19, 29...

So now, you will have a new integer sequence: 1, 2, 3, 4, 5, 6, 7, 8, 10, 11,
...

Given a positive integer `n`, you need to return the n-th integer after
removing. Note that 1 will be the first integer.

**Example 1:**

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Input: 9
Output: 10
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Solution1
---------

题目输入的n，代表1\~n的这些数都会依次输入到该算法中，该算法需要删除这些输入中包含9的数。在进一步分析会发现，这道题目其实是基数的问题（9），关于基数的题，有固定的算法模板：

-   取模来控制最低位

-   乘模调整base

-   累加保存结果

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ java
public class Solution {
    public int newInteger(int n) {
        int ans = 0;
        int base = 1;
        while(n > 0){
            ans += (n % 9 * base);
            n /= 9;
            base *= 10;
        }
        return ans;
    }
}
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

 

**enjoy life, coding now! :D**
