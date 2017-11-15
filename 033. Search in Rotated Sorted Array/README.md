# 033.  Search in Rotated Sorted Array

# Solution

![](http://www.tangjikai.com/uploads/2/7/7/3/27735981/4956640_orig.png)

我们需要区分mid的值是处于哪种情况，然后还是做二分搜索。正常情况，二分都是在有序的数组中进行的，但是在这种对有序数组进行rotated之后的数组，仍然可以进行二分搜索，只是在做比较的时候需要多做几次比较。

```java
class Solution {
    public int search(int[] nums, int target) {
        if(nums == null || nums.length == 0) return -1;
        int l = 0, r = nums.length-1;
        while(l <= r){
            int mid = l + (r-l)/2;
            if(nums[mid] == target){
                return mid;
            }else if(nums[mid] > nums[r]){
                if(target >= nums[l] && target < nums[mid]){
                    r = mid - 1;
                }else{
                    l = mid + 1;
                }
            }else{
                if(target > nums[mid] && target <= nums[r]){
                    l = mid + 1;
                }else{
                    r = mid - 1;
                }
            }
        }
        return -1;
    }
}
```

