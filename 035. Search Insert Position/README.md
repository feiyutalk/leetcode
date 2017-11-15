# 035. Search Insert Position

# Solution

这道题目的本质还是属于二分搜索问题，我们需要找的是第一个大于等于target的元素下标。这样我们套用大于等于的搜索问题的模板进行求解。

```java
class Solution {
    public int searchInsert(int[] nums, int target) {
        if(nums == null || nums.length == 0) return 0;
        int l = 0, r = nums.length;
        while(l < r){
            int mid = l + (r-l)/2;
            if(nums[mid] >= target){
                r = mid;
            }else{
                l = mid + 1;
            }
        }
        return l;
    }
}
```

