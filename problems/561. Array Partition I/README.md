# 561. Array Partition I

# Description

Given an array of **2n** integers, your task is to group these integers into **n** pairs of integer, say (a1, b1), (a2, b2), ..., (an, bn) which makes sum of min(ai, bi) for all i from 1 to n as large as possible.

**Example 1:**

```
Input: [1,4,3,2]

Output: 4
Explanation: n is 2, and the maximum sum of pairs is 4 = min(1, 2) + min(3, 4).

```

# Solution

题目的意思就是输入的数据集肯定是偶数个，可以两两组成一对，假设有2n个数据，就可以组成n对，然后每一对里面取出一个最小的，将这n个最小值相加得到一个值，我们希望这个值最大。

很自然的想法就是对数组先排序，然后每隔2个位置取一个值，加到result中，最后返回result。

看了下是easy的题目，自己写了个选择排序，结果超时了，，，最后还是用了Java自带的Arrays.sort()。这道题目，有两个其实：

1. 看Java源码，用什么实现排序算法的。
2. 熟悉各种排序算法，特别是快速排序。

```java
class Solution {
    public int arrayPairSum(int[] nums) {
        //boundary condition
        if(nums == null || nums.length == 0)
            return 0;
        //normal condition
        Arrays.sort(nums);
        int sum = 0;
        for(int i=0; i<nums.length; i+=2){
            sum += nums[i];
        }
        return sum;
    }
}
```

