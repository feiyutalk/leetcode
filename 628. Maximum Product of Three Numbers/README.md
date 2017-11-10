# 628. Maximum Product of Three Numbers

# Solution

这道题目其实没有什么难度，先对数组进行排序然后取最大的三个值相乘就可以了。但是这里有个陷阱，就是当出现下面这种情况的时候:

`[-4,-3,-2,-1,60]`

也就是正数只有1个，其他都是负数的时候，会发现上面的算法就失效了，这种情况下，应该取最小的那两个负数，所以我们需要多加一个判断条件。

```java
class Solution {
    public int maximumProduct(int[] nums) {
        //boundary condition
        if(nums == null || nums.length == 0) return 0;
        //normal condition
        Arrays.sort(nums);
        int l = nums.length;
        int a = nums[l-1]*nums[l-2]*nums[l-3];
        int b = nums[0]*nums[1]*nums[l-1];
        return Math.max(a, b);
    }
}
```

