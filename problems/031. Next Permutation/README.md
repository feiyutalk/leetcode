# 031. Next Permutation

```java
class Solution {
    public void nextPermutation(int[] nums) {
        if(nums == null || nums.length == 0) return;
        int replace = nums.length - 2;
        while(replace >= 0){
            if(nums[replace] < nums[replace+1]) break;
            replace--;
        }
        if(replace < 0){
            Arrays.sort(nums);
            return;
        }
        int lgrIdx = replace + 1;
        while(lgrIdx < nums.length && nums[lgrIdx] > nums[replace]){
            lgrIdx++;
        }
        int temp = nums[replace];
        nums[replace] = nums[lgrIdx-1];
        nums[lgrIdx-1] = temp;
        Arrays.sort(nums, replace+1, nums.length);
    }
}
```

