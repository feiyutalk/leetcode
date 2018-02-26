# 300. Longest Increasing Subsequence

## \#1 Brute Force[TLE]

暴力搜索的想法是对于每个元素，有选或不选两种可能，其中要选择该元素，需要满足该元素值比上一个递增序列的最后一个元素值来得大，所以需要传递一个变量来记录上一个递增序列的最后一个值。虽然想法比较直接，但是时间复杂度过高，达到$O(2^n)$。

```java
class Solution {
    public int lengthOfLIS(int[] nums) {
        return lengthOfLIS(nums, Integer.MIN_VALUE, 0);
    }
    
    public int lengthOfLIS(int[] nums, int prev, int curpos){
        if(curpos == nums.length) return 0;
        int taken = 0;
        if(nums[curpos] > prev)
            taken = 1 + lengthOfLIS(nums, nums[curpos], curpos+1);
        int notaken = lengthOfLIS(nums, prev, curpos+1);
        return Math.max(taken, notaken);
    }
}
```

## \#2 Recursion with memorization[AC]

在第一种方法中，递归的过程里会重复计算很多参数相同的函数，这会造成时间上的浪费，这里通过一个缓冲数组来记录已经计算过的值，下次需要计算某个函数的时候，先在缓存中找是否有该值，如果有直接取即可，无需再次计算；如果没有，先计算该值，然后放到缓存中。

```java
public class Solution {
    public int lengthOfLIS(int[] nums) {
        int memo[][] = new int[nums.length + 1][nums.length];
        for (int[] l : memo) {
            Arrays.fill(l, -1);
        }
        return lengthofLIS(nums, -1, 0, memo);
    }
    public int lengthofLIS(int[] nums, int previndex, int curpos, int[][] memo) {
        if (curpos == nums.length) {
            return 0;
        }
        if (memo[previndex + 1][curpos] >= 0) {
            return memo[previndex + 1][curpos];
        }
        int taken = 0;
        if (previndex < 0 || nums[curpos] > nums[previndex]) {
            taken = 1 + lengthofLIS(nums, curpos, curpos + 1, memo);
        }

        int nottaken = lengthofLIS(nums, previndex, curpos + 1, memo);
        memo[previndex + 1][curpos] = Math.max(taken, nottaken);
        return memo[previndex + 1][curpos];
    }
}
```

