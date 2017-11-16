# 034. Search for a Range

# Solution

二分搜索问题中关于范围的搜索，我们可以将范围的搜索归结于该范围start和end两个值的搜索，对于start的，我们可以采用大于等于的二分搜索算法，对于end，我们可以采用小于等于的二分搜索算法。

```java
class Solution {
    public int[] searchRange(int[] nums, int target) {
        if(nums == null || nums.length == 0)
            return new int[]{-1,-1};
        int[] res = new int[2];
        //search start point
        int l = 0, r = nums.length;
        while(l < r){
            int mid = l + (r - l)/2;
            if(nums[mid] >= target){
                r = mid;
            }else{
                l = mid + 1;
            }
        }
        if(l == nums.length || nums[l] != target)
            res[0] = -1;
        else{
            res[0] = l;
        }
        
        l = -1; 
        r = nums.length-1;
        while(l < r){
            int mid = l + (r - l + 1)/2;
            if(nums[mid] <= target){
                l = mid;
            }else{
                r = mid - 1;
            }
        }
        if(r == -1 || nums[r] != target)
            res[1] = -1;
        else{
            res[1] = r;
        }
        return res;
    }
}
```

