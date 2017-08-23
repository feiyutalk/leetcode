#  410. Split Array Largest Sum

## Description

```
Difficulty: Hard
Total Accepted:13.5K
Total Submissions:36.7K
Contributor: LeetCode
```
Given an array which consists of non-negative integers and an integer m, you can split the array into m non-empty continuous subarrays. Write an algorithm to minimize the largest sum among these m subarrays.

Note:
If n is the length of array, assume the following constraints are satisfied:

- 1 ≤ n ≤ 1000

- 1 ≤ m ≤ min(50, n)


**Examples:**

```
Input:
nums = [7,2,5,10,8]
m = 2

Output:
18

Explanation:
There are four ways to split nums into two subarrays.
The best way is to split it into [7,2,5] and [10,8],
where the largest sum among the two subarrays is only 18.
```

***
## Solution1 负相关的二分求解
  这道题目确实非常有难度，难度点在于对问题的建模，如何找到最大值的最小值val和m的关系，它们之间是一个负相关的关系，也就是val越大，m越小。所有val和m是满足单调递减的函数关系，我们还是可以用二分的方法去猜答案，每次都猜中点，这里还是要用反函数的做法，就是固定m，反向猜val。我们可以将二分法的框架用于这类题目中，我们默认规定的区间是左闭右开的区间，写好guess函数是这道题目的关键，也是所有二分问题的出题点。

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

**enjoy life, coding now! :D**
