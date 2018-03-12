# 55. Jump Game

## #1 暴力搜索[TLE]

在每个位置上，我们可以遍历下一次可以走的每个位置，这个范围为`[step+1, step+nums[step])]`，如果最后`step >= nums.length - 1`说明是可以走到终点的；如果遍历完所有的范围都不行， 那说明不能走到终点。

```java
class Solution {
    public boolean canJump(int[] nums) {
        if(nums == null || nums.length == 0)
            return false;
        return helper(nums, 0);
    }
    
    private boolean helper(int[] nums, int step){
        if(step >= nums.length - 1)
            return true;
        int furtherst = Math.min(step+nums[step], nums.length-1);
        for(int i=step+1; i<=furtherst; i++){
            if(helper(nums, i))
                return true;
        }
        return false;
    }
}
```

## #2 贪心[AC]

```java
class Solution {
    public boolean canJump(int[] nums) {
        if(nums == null || nums.length == 0)
            return false;
        int reach = 0;
        for(int i=0; i<nums.length && i<=reach; i++){
            reach = Math.max(reach, nums[i]+i);
            if(reach >= nums.length-1) return true;
        }
        return false;
    }
}
```

