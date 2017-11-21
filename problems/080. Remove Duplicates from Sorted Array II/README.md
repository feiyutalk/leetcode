# 80. Remove Duplicates from Sorted Array II

和删除重复元素类似，这边最多可以保留两个，那么我遍历就从`i=2`开始，然后呢，`nums[i]`和`nums[tail-1]`和`nums[tail-2]`比较，如果有一个不同的话，就可以加入了。

```java
class Solution {
    public int removeDuplicates(int[] nums) {
        if(nums == null || nums.length < 2)
            return nums.length;
        int tail = 2;
        for(int i=2; i<nums.length; i++){
            if(nums[i] != nums[tail-1] || nums[i] != nums[tail-2]){
                nums[tail] = nums[i];
                tail += 1;
            }
        }
        return tail;
    }
}
```

