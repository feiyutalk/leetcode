# 724. Find Pivot Index

```Java
class Solution {
    public int pivotIndex(int[] nums) {
        if(nums == null || nums.length == 0)
            return -1;
        // init left sum and right sum
        int leftSum = 0;
        int rightSum = 0;
        for(int num : nums)
            rightSum += num;
        for(int i=0; i<nums.length; i++){
            rightSum -= nums[i];
            if(leftSum == rightSum) return i;
            leftSum += nums[i];
        }
        return -1;
    }
}
```



