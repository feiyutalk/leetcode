# 11. Container With Most Water
## Description

```
Difficulty: Medium
```

Given n non-negative integers a1, a2, ..., an, where each represents a point at coordinate (i, ai). n vertical lines are drawn such that the two endpoints of line i is at (i, ai) and (i, 0). Find two lines, which together with x-axis forms a container, such that the container contains the most water.

Note: You may not slant the container and n is at least 2.
## Solution 1
我们需要知道，题目的意思是去求解矩形的最大面积，我们怎么去求解得到最大面积的矩形呢？如果我们采用穷举的方式，那这时候的时间复杂度是O(n^2)。除了枚举，我们是否还有其他的方法呢？

我们可以定义两个下标left,right。初始化时，left是最左边的下标0,right是最右边的下标length-1。紧接着，我们每次都移动高度较小的对应的下标，其中left++，right--。为什么可以这样做呢？也就是为什么要移动较小的那个呢？

假设我移动较大那个高度对应的下标，此时有两种情况出现

1. 移动后得到的高度大于原来的高度，但是此时高度还是以之前较小的那个高度为准，而此时的宽度比之前的宽度小。
2. 移动后得到的高度小于原来的高度，那此时不仅高度比原来小，宽度还比原来小。

所以我们移动较高的那个下标得到的矩形都比原来的小。这种方式得到的时间复杂度为O(n)。

```java

class Solution {
    public int maxArea(int[] height) {
        // boundary condition
        if(height == null || height.length == 0)
            return 0;
        // normal condition
        int left = 0;
        int right = height.length-1;
        int area = 0;
        while(left < right){
            area = Math.max(area, Math.min(height[left], height[right]) * (right -left));
            if(height[left] < height[right]){
                left++;
            }else if(height[left] > height[right]){
                right--;
            }else{
                left++;
                right--;
            }
        }
        return area;
    }
}
```

***

**enjoy life, coding now! :D**
