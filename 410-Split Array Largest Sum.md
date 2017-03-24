#Description

:star2::star2::star2:

![](/images/Split_Array_Largest_Sum.png)

***
##Analysis
这道题目确实非常有难度，难度点在于对问题的建模，如何找到最大值的最小值val和m的关系，它们之间是一个负相关的关系，也就是val越大，m越小。所有val和m是满足单调递减的函数关系，我们还是可以用二分的方法去猜答案，每次都猜中点，这里还是要用反函数的做法，就是固定m，反向猜val。我们可以将二分法的框架用于这类题目中，我们默认规定的区间是左闭右开的区间，写好guess函数是这道题目的关键，也是所有二分问题的出题点。

##Solution 负相关的二分求解

```java
public class Solution {
    public boolean guess(long mid, int[] nums, int m){
        long sum = 0;
        for(int i=0; i<nums.length; i++){
            if(nums[i] > mid)
                return false;
            if(sum + nums[i] > mid){
                m--;
                sum = nums[i];
            }else{
                sum += nums[i];
            }
        }
        return m >= 1;
    }
    
    public int splitArray(int[] nums, int m) {
        long low = 0l;
        long high = 1l;
        long mid = 0l;
        int ans = 0;
        for(int i=0; i<nums.length; i++){
            high += nums[i];
        }
        while(low < high){
            mid = (low + high)/2;
            if(guess(mid, nums, m)){
                ans = (int)mid;
                high = mid;
            }else{
                low = mid + 1;
            }
        }
        return ans;
    }
}
```
***
enjoy life, coding now! :D
