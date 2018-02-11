# 53. Maximum Subarray

## Solution 1 暴力搜索[TLE]

该解法枚举出所有的可能情况，穷举所有的解空间，也是遍历所有可能的连续子数组，求得所有连续子数组的和，然后作比较，得到最大的和。时间复杂度达到了 $O(n^3)$，想法简单，直接，但是时间复杂度较高。

```java
class Solution {
    public int maxSubArray(int[] nums) {
        if(nums == null || nums.length == 0)
            return 0;
        int max = Integer.MIN_VALUE;
        for(int i=0; i<nums.length; i++){
            for(int j=i; j<nums.length; j++){
                int sum = 0;
                for(int k=i; k<=j; k++){
                    sum += nums[k];
                }
                if(sum > max)
                    max = sum;
            }
        }
        return max;
    }
}
```

对于时间复杂度的总结如下：![](./images/时间复杂度总结.png)

## Solution 2 优化枚举[TLE]
我们通过分析解法1发现，对于:

```java
for(int k=i; k<j; k++){
  sum += nums[k];
}
```

这段最内层的代码，我们在计算sum的时候，其实可以采用**增量**的方式。在计算 nums[1] + nums[2] +nums[3]的时候，可以在 (nums[1] + nums[2])的基础上，加上nums[3], 而不需要重头去遍历数组，这样会多了很多操作，所有我们，对最内层的循环进行优化，**采用增量的方式，减少一层循环**。

```java
class Solution {
    public int maxSubArray(int[] nums) {
        if(nums == null || nums.length == 0)
            return 0;
        int max = Integer.MIN_VALUE;
        for(int i=0; i<nums.length; i++){
            int sum = 0;
            for(int j=i; j<nums.length; j++){
                sum += nums[j];
                if(sum > max)
                    max = sum;
            }
        }
        return max;
    }
}
```

时间复杂度$O(n^2)$

当我们洋洋得意时，leetcode却给了我们一个超时的警告:fearful::

![](./images/两重循环超时.png)

## Solution 3 贪心算法[AC]
我们虽然对枚举进行的优化，但是枚举终究还是枚举，是最坏的算法了，它去遍历整个解空间，这样的做法有些愚蠢，我们该怎么做才能缩小解空间，得到我们需要的解？:thinking:
这时候就需要用我们的数学思想去缩小我们的解空间了，想啊想，我这里想到的是 **主要矛盾思想**， 怎么说呢，我们知道最大子数组的特点是什么，这是问题最最主要的矛盾点，那就是任一前缀都不可能小于0，你想啊，如果有任意前缀小于0，那我把那个前缀换成0（也就是不要这个前缀嘛），不就得到更大的子数组了吗！:stuck_out_tongue_closed_eyes: 在这里被称为贪心算法，这一主要矛盾的发现，极大的缩小了我们搜索解空间的范围，从而降低了事件复杂度。

```java
class Solution {
    public int maxSubArray(int[] nums) {
        if(nums == null || nums.length == 0)
            return 0;
        int max = Integer.MIN_VALUE;
        int sum = 0;
        for(int i=0; i<nums.length; i++){
            sum += nums[i];
            if(sum > max)
                max = sum;
            if(sum < 0) 
                sum = 0;
        }
        return max;
    }
}
```

时间复杂度:$O(n)$

## Summary 以上三种算法

通过以上的三种解答的分析，我们应该知道对于算法题目，最直接的想法就是穷举，如果发现穷举得到的时间复杂度不行，那么我们就要想办法进行优化，对于循环层数多的算法，优化点往往在最内层的循环，这里用到了一个增量的方式来代替一层循环，又学到了一招:laughing:。如果优化后，还是不行的话，那么就需要一些数学上的思想或者技巧来解决了，这确实有点难，但是日积月累，最后就会掌握很多思想和技巧，就能极大的缩小我们的解空间了，最后，来看看贪心算法的威力吧:

![](./images/贪心算法的威力.png)

## Solution 4 动态规划

这道题目可以用动态规划来求解，我们定义状态`dp[i]`表示最后一个元素为`nums[i]`的连续子数组中的最大和。对于转移方程，`dp[i]`可能由`dp[i-1]+nums[i]`或`nums[i]`得到，我们只需要再两者中求最大的即可。整个算法的时间复杂度为$O(n)$.

```java
class Solution {
    public int maxSubArray(int[] nums) {
        if(nums == null || nums.length == 0)
            return 0;
        int[] dp = new int[nums.length]; // dp[i] 代表最后一个元素为nums[i]的连续子数组的最大和
        dp[0] = nums[0]; //dp[0] 最后一个元素为nums[0]
        int max = nums[0];
        for(int i=1; i<nums.length; i++){
            dp[i] = Math.max(dp[i-1] + nums[i], nums[i]);
            max = Math.max(max, dp[i]);
        }
        return max;
    }
}
```

