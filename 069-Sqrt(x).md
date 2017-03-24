#Description

:star2:

![](/images/Sqrt.png)
***
##Analysis
这道题目当然可以遍历求解，从0到x/2,依次遍历，如果其平方小于等于给定的x，则继续增加，这样可以得到结果，时间复杂度为O(n)，当然，我们可以用二分法来求解，为什么呢？因为 f(x) = x^1/2 这个函数是一个单调增的函数，这意味着当我们增大自变量时，因变量也随之增大，反之亦然。这样的条件，使得我们可以去猜一个答案，然后去调整这个答案。因为函数单调性的性质，所以调整的方向是唯一的，而猜这个答案最好的方式的平均，这在博弈论证实过的结论。所以，这也是二分法一般的规律吧。顺带说一句，这道题直接 return (int)Math.sqrt(x); 竟然也AC了。。。

##Solution 二分求解

```java
public class Solution {
    public int mySqrt(int y) {
       long low = 0l;
       long high = (long)y;
       long mid = 0l;
       long ans = 0l;
       while(low <= high){
           mid  = (low + high)/2;
           if(mid * mid <= y){
               ans = mid;
               low = mid + 1;
           }else{
               high = mid - 1 ;
           }
       }
       return (int)ans;
    }
}   
```
***
enjoy life, coding now! :D
