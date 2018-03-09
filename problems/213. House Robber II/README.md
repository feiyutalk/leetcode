# 213. House Robber II

## #1 动态规划[AC]

这道题目的特点是，由于首尾相互连接，所以偷不偷有两种可能的搜索路径。对于这两种搜索路径， 其使用的搜索方法都是一样的，详见[leetcode198解题报告](https://github.com/conghuaicai/leetcode/tree/master/problems/198.%20House%20Robber)。

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

#### 复杂性分析：

- **时间复杂性：**$O(n)$

- **空间复杂性：**$O(n)$

  ​