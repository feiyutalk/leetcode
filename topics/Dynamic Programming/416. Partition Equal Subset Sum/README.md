# 416. Partition Equal Subset Sum

# Description

Given a **non-empty** array containing **only positive integers**, find if the array can be partitioned into two subsets such that the sum of elements in both subsets is equal.

**Note:**

1. Each of the array element will not exceed 100.
2. The array size will not exceed 200.

**Example 1:**

```
Input: [1, 5, 11, 5]

Output: true

Explanation: The array can be partitioned as [1, 5, 5] and [11].
```

**Example 2:**

```
Input: [1, 2, 3, 5]

Output: false

Explanation: The array cannot be partitioned into equal sum subsets.
```

# Solution

第一眼看到这个题目，想到的方法是用子集枚举的模板来做的，在我们的枚举过程中，将被枚举到的元素当成第一个集合，剩下的元素当成第二个集合，这样的时间复杂度是O(n2)，由于算法的模板之前有总结过，写起来也是比较快的，但是提交的时候报了超时。

```java
class Solution {
    private boolean find = false;
    public boolean canPartition(int[] nums) {
        //boundary condition
        if(nums == null || nums.length == 0)
            return true;
        //normal condition
        int first = 0;
        int total = 0;
        for(int num : nums)
            total += num;
        backtrack(nums, first, total, 0);
        return find;
    }
    
    private void backtrack(int[] nums, int first, int total, int step){
        if(first * 2 == total){
            find = true;
            return;
        }else{
            for(int i=step; i<nums.length; i++){
                first += nums[i];
                backtrack(nums, first, total, i+1);
                if(find)
                    return;
                first -= nums[i];
            }
        }
    }
}
```

那就不能用O(nums2)时间复杂度的算法来求解了，所以基于枚举的方法是不可行的。这种算法的时间复杂度是元素个数的平方。

现在考虑用动态规划的方法来求解，如果是动态规划的话，时间复杂度就是O(nums*target)，实际上，时间复杂度也差不多，而且还需要同样的空间。

其实这道题目和之前做过的一道题目类似，问的是在一个集合中，能不能找到一些数，相加等于一个给定的值，这里把这个给定的值设为所有元素和的一半。

做动态规划的题，需要回答以下几个问题:

- 动态规划中的状态是什么？怎么定义的。
- 动态规划的初始状态的值是多少？
- 动态规划的转化方程怎么定义？

我们结合这道题来回答这个问题:

- 我们定义状态是，用当前这个集合内的元素，是否可以选择出一些元素，它们相加等于这个给定的值。这个状态定义有一个规律，就是和我们的题目中的input,output是一样的，比如，这道题问的是，给出一个集合[….]是否可以选择出一个元素，它们相加等于所有元素之和的一半，当然了，题目的状态是我们要走到的最后一个状态，我们需要从已知状态一步步走到未知的状态。
- 既然明确了我们的目标，紧接着，我们需要得出，我们现在的已知状态是什么？我们先构建出状态图:这边以输入时[1,2,3,6]为例子

|      | 1    | 2    | 3    | 4    | 5    | 6    |
| :--: | ---- | ---- | ---- | ---- | ---- | ---- |
|  1   |      |      |      |      |      |      |
|  2   |      |      |      |      |      |      |
|  3   |      |      |      |      |      |      |
|  6   |      |      |      |      |      |      |

​	我们一开始已知的通常都是状态图最初的状态值，这里的一个技巧就是通常考虑，第一行，第一列的值，所以，加上初始状态后，我们的状态图变成如下的值:

|      | 0    | 1     | 2     | 3     | 4     | 5     | 6     |
| :--: | ---- | ----- | ----- | ----- | ----- | ----- | ----- |
|  1   | True | False | False | False | False | False | False |
|  2   | True |       |       |       |       |       |       |
|  3   | True |       |       |       |       |       |       |
|  6   | True |       |       |       |       |       |       |

- 既然有了状态的定义，以及一些已知的状态，现在就需要给出状态转换的方程了，我们现在考虑用[1,2]来求目标值1的情况，这时候发现`num[i] > j`，说明什么问题，说明我们先加入的元素值，比目标值大，这样的话，这个元素值是不能取的，所以有 `dp[i][j]=dp[i-1][j] `；如果考虑用[1,2]来求目标值6的情况，这是我们有两种情况要考虑，取2或者不取2，不取2的情况和上面一样；取2的情况下，就把问题转化为已知的`dp[i-1][j-nums[i]]`这种已知的情况。

所以，通过对上面的分析，我们基本可以发现，动态规划的特点就是先定义状态和确定初始状态，然后考虑转化方程，对于一个新状态，我们通常需要用分类讨论等方法将新状态转化为若干个已知状态的组合。

```java
class Solution {
    private boolean find = false;
    public boolean canPartition(int[] nums) {
        //boundary condition
        if(nums == null || nums.length == 0)
            return true;
        //normal condition
        int total = 0;
        for(int num : nums)
            total += num;
        if(total%2 != 0)
            return false;
        
        int target = total/2;
        // dp
        // init
        boolean[][] dp = new boolean[nums.length][target+1];
        // init first row
        if(nums[0] <= target) dp[0][nums[0]] = true;
        // init first col
        for(int i=0; i<nums.length; i++)
            dp[i][0] = true;
        // transaction
        for(int i=1; i<dp.length; i++){
            for(int j=1; j<dp[0].length; j++){
                if(nums[i] > j){
                    dp[i][j] = dp[i-1][j];
                }else{
                    dp[i][j] = dp[i-1][j-nums[i]] || dp[i-1][j];
                }
            }
        }
        
        return dp[dp.length-1][dp[0].length-1];
    }
    
}
```

