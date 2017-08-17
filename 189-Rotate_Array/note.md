# 189. Rotate Array
## Description

```
Difficulty: Easy
```

Rotate an array of n elements to the right by k steps.

For example, with n = 7 and k = 3, the array [1,2,3,4,5,6,7] is rotated to [5,6,7,1,2,3,4].

## Solution 1
  这个解法用到了数学上转置的一些技巧：


	input = [1,2,3,4,5,6,7] 我们定义 A = [1,2,3,4] B = [5,6,7]
	expect = [5,6,7,1,2,3,4]----> [BA]
	我们需要从[AB] ---> [BA]
	怎么做呢？
	[A`B`]` ---->  [BA]

下面是代码：

	public class Solution {
	    public void rotate(int[] nums, int k) {
	        if(nums == null || nums.length == 0)
	            return;
	        int n = nums.length;
	        if(k >= n)
	            k %= n;
	        rotate(nums,0, n-k-1);
	        rotate(nums,n-k, n-1);
	        rotate(nums,0,n-1);
	    }
	
	    public void rotate(int[] nums, int start, int end){
	        for(int i=start, j=end; i<j; i++, j--){
	            int temp = nums[i];
	            nums[i] = nums[j];
	            nums[j] = temp;
	        }
	    }
	}

***

**enjoy life, coding now! :D**
