# 026. Remove Duplicates from Sorted Array

这道题目还是可以采用前向指针法，这里删除重复元素，使其只保留一个就可以了。我们可以使用前向指针法中的`tail`指针来做。

```java
class Solution {
    public int removeDuplicates(int[] nums) {
        if(nums == null || nums.length == 0)
            return 0;
        int tail = 1;
        for(int i=0; i<nums.length; i++){
            if(nums[i] != nums[tail-1]){
                nums[tail] = nums[i];
                tail += 1;
            }
        }
        return tail;
    }
}
```

