#Descreption

:star2::star2:

Find the contiguous subarray within an array (containing at least one number) which has the largest product.

For example, given the array [2,3,-2,4],
the contiguous subarray [2,3] has the largest product = 6.

***
##Analysis
之前做过最大子数组和的问题，那道题的主要矛盾点在于，如果是最大子数组和，那么它的任意前缀都不可能小于0，否则不要这个前缀（也就是把这个前缀置位0），那么将得到更大的子数组和。和这个问题做对比，显然，最大子数组积更加复杂，那么复杂在哪里？复杂在于两个负数的乘积有可能大于两个正数的乘积，说白了，就是现在的最大值不只是取决于正数了，也有可能是负数因子的影响？那么什么情况下会是负数因子产生的最大值呢？我们用分类整合的思想对问题进行分解，讨论如下：


最大值有两种情况产生：

1. 如果当前是正数：

	A = 当前值   B = 当前值 × 之前的最大值
则我们可以知道，在当前是正数的情况下， 最大值 = Max(A, B)
2. 如果当前是负数：

	A = 当前值   B = 当前值 × 之前的最小值
则我们可以知道，在当前是负数的情况下， 最大值 = Max(A, B)

所以，我们必须记录下之前的最小值，最大值，然后对每个遍历过的值进行分类整合。

##Solution 分类整合思想

```java
public class Solution {
    public int maxProduct(int[] nums) {
        if(nums.length == 0 || nums == null)
            return 0;
        int maxpre = nums[0];
        int minpre = nums[0];
        int maxtemp = nums[0];
        int mintemp = nums[0];
        int max = nums[0];
        for(int i=1; i<nums.length; i++){
            if(nums[i] >= 0){
                maxtemp  = Math.max(maxpre*nums[i], nums[i]);
                mintemp = Math.min(minpre*nums[i], nums[i]);                
            }else{
                maxtemp = Math.max(minpre*nums[i], nums[i]);
                mintemp = Math.min(maxpre*nums[i], nums[i]);
            }
            maxpre = maxtemp;
            minpre = mintemp;
            max = Math.max(maxtemp, max);
        }
        return max;
    }
}
```

```math
时间复杂度： O(n)
```
***
enjoy life, coding now! :D 
