#Desciption
```
Find the contiguous subarray within an array (containing at least one number) which has the largest sum.

For example, given the array [-2,1,-3,4,-1,2,1,-5,4],
the contiguous subarray [4,-1,2,1] has the largest sum = 6.
```
***
##Solution 1 暴力求解法

```java
public class Solution {
    public int maxSubArray(int[] nums) {
        int max = -2147483647;
        for(int i=0; i<nums.length; i++){
            for(int j=i+1; j<=nums.length; j++){
                int sum = 0;
                for(int k=i; k<j; k++){
                    sum += nums[k];
                }
                if(sum > max){
                    max = sum;     
                }
            }
        }
        return max;
    }
}
```
##Analysis
枚举出所有的可能情况，穷举所有的解空间，时间复杂度达到了O(n^3)，这属于比较差的时间复杂度，有优化的空间。对于时间复杂度的总结如下：

![](/images/Maximum_Subarray/时间复杂度总结.png)

***
##Improve
我们通过分析方法一发现，对于:

```java
                for(int k=i; k<j; k++){
                    sum += nums[k];
                }
```

这段最内层的代码，我们在计算sum的时候，其实可以采用增量的方式，也就是我们在计算 nums[1] + nums[2] +nums[3]的时候，可以在 (nums[1] + nums[2])的基础上，加上nums[3], 而不需要重头去遍历数组，这样会多了很多操作，所有我们，对最内层的循环进行优化，采用增量的方式，减少一层循环。

##Solution 2 优化枚举
```java
public class Solution {
    public int maxSubArray(int[] nums) {
        int max = -2147483647;
        for(int i=0; i<nums.length; i++){
            int sum = 0;
            for(int j=i+1; j<=nums.length; j++){
                sum += nums[j-1];
                if(sum > max){
                    max = sum;     
                }
            }
        }
        return max;
    }
}
```
当我们洋洋得意时，leetcode却给了我们一个超时的警告:fearful::

![](/images/Maximum_Subarray/两重循环超时.png)

***