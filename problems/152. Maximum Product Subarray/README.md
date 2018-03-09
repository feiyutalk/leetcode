# 152. Maximum Product Subarray

## #1 动态规划[AC]

常见的动态规划题一般只有一个状态空间，但是我们的思维不能被固化，不然遇到新的问题就容易求解不出来。这道题目用动态规划求解的时候，需要两个状态空间，其中一个状态空间`minDP[i]`记录的是以第`i`个元素结尾的连续子数组的最小值，而另一个状态空间`maxDP[i]`记录的是以第`i`个元素结尾的连续子数组的最大值，这么做的原因在于负数*负数为正数的情况。也就是，如果当前元素是负数的话，那么让它乘以之前的最小负数，将会得到一个很大的正数。

```java
class Solution {
    public int maxProduct(int[] nums) {
        if(nums == null || nums.length == 0)
            return 0;
        int[] minDP = new int[nums.length];
        int[] maxDP = new int[nums.length];
        minDP[0] = nums[0];
        maxDP[0] = nums[0];
        int res = nums[0];
        for(int i=1; i<nums.length; i++){
            minDP[i] = Math.min(Math.min(minDP[i-1]*nums[i], maxDP[i-1]*nums[i]), nums[i]);
            maxDP[i] = Math.max(Math.max(minDP[i-1]*nums[i], maxDP[i-1]*nums[i]), nums[i]);
            res = Math.max(res, Math.max(minDP[i], maxDP[i]));
        }
        return res;
    }
}
```

#### 复杂性分析：

- **时间复杂性：**$O(n)$

- **空间复杂性：**$O(n)$

  ​