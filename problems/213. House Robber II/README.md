# 213. House Robber II

```java
class Solution {
    public int rob(int[] nums) {
        if(nums.length == 1) return nums[0];
        return Math.max(doRob(nums, 0, nums.length-2), doRob(nums, 1, nums.length - 1));
    }
    
    private int doRob(int[] nums, int l, int h){
        int prevNo = 0;
        int prevYes = 0;
        for(int i=l; i<=h; i++){
            int temp = prevNo;
            prevNo = Math.max(prevNo, prevYes);
            prevYes = nums[i] + temp;
        }
        return Math.max(prevNo, prevYes);
    }
}
```

