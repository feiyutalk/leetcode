# 665. Non-decreasing Array
## Description

```
Difficulty: Easy
```
Given an array with n integers, your task is to check if it could become non-decreasing by modifying at most 1 element.

We define an array is non-decreasing if array[i] <= array[i + 1] holds for every i (1 <= i < n).

Example 1:

	Input: [4,2,3]
	Output: True
	Explanation: You could modify the first 4 to 1 to get a non-decreasing array.

Example 2:

	Input: [4,2,1]
	Output: False
	Explanation: You can't get a non-decreasing array by modify at most one element.
## Solution 1
  首先，我们需要最多修改一个元素就能得到一个非递减的数组。如果我们有2个元素是不符合非递减的要求的，也就是在它后面有元素比它小。这个时候，我们从后往前调整元素，我们先调整最后一个，因为后面有元素比它小，所以肯定需要往下调整（值变小）。所以，该调整之后，没有影响到前面不满足条件的元素，因为是向下调整，所有前面不满足条件的元素仍然是不满足条件的。所以，我们发现，如果有两个元素不满足条件，那就无法通过一次修改来得到非递减的数组。但是，我们会发现如果是这样的序列 [3,3,2] 其实上，虽然两个3都不满足条件，但是却可以修改2就得到非递减的数组。所有，我们不仅从前往后判断，还需要从后往前判断。

```java

class Solution {
    public boolean checkPossibility(int[] nums) {
        int count = 0;
        for(int i=0; i<nums.length-1; i++){
            for(int j=i+1; j<nums.length; j++){
                if(nums[i] > nums[j]){
                    count++;
                    break;
                }
            }
        }
        if(count <= 1){
            return true;
        }
        
        count = 0;
        for(int i=nums.length-1; i>0; i--){
            for(int j=i-1; j>=0; j--){
                if(nums[i] < nums[j]){
                    count++;
                    break;
                }
            }
        }
        
        if(count <= 1){
            return true;
        }
        return false;
    }
}

```

***

**enjoy life, coding now! :D**
