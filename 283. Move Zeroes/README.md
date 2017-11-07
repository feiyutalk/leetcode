# 283. Move Zeroes

# Solution

题目要求我们把所有的0移到数组的最右边，这里一次遍历，将遍历到的0元素和后面第一次出现的非0元素交换，最后能将所有的非零元素都交换到0元素的前面。

```java
class Solution {
    public void moveZeroes(int[] nums) {
        if(nums == null || nums.length == 0)
            return;
        for(int i=0; i<nums.length; i++){
            if(nums[i] == 0){
                for(int j=i+1; j<nums.length; j++){
                    if(nums[j] != 0){
                        int temp = nums[i];
                        nums[i] = nums[j];
                        nums[j] = temp;
                        i--;
                        break;
                    }
                }
            }
        }
    }
}
```

