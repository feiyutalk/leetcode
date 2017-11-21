# 075. Sort Colors

使用双向指针法，分别记录`red`和`blue`的颜色数量。

```java
class Solution {
    public void sortColors(int[] nums) {
        //0 1 2 red white blue
        if(nums == null || nums.length == 0)
            return;
        int i=0, red = 0, blue = nums.length - 1;
        while(i <= blue){
            if(nums[i] == 0){
                int temp = nums[red];
                nums[red] = nums[i];
                nums[i] = temp;
                red += 1;
            }else if(nums[i] == 2){
                int temp = nums[blue];
                nums[blue] = nums[i];
                nums[i] = temp;
                blue -= 1;
                i -= 1;
            }
            i += 1;
        }
    }
}
```

需要注意，为什么和后面的数进行交换的时候需要执行`i -= 1`，因为后面的数我们并没有遍历过，而前面的数我们都是处理过的，都是等于red的。