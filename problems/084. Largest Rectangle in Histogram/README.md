# 084. Largest Rectangle in Histogram 

# Description

Given *n* non-negative integers representing the histogram's bar height where the width of each bar is 1, find the area of largest rectangle in the histogram.

![](https://leetcode.com/static/images/problemset/histogram.png)

Above is a histogram where width of each bar is 1, given height = `[2,1,5,6,2,3]`.

![](https://leetcode.com/static/images/problemset/histogram_area.png)

The largest rectangle is shown in the shaded area, which has area = `10` unit.

For example,
Given heights = `[2,1,5,6,2,3]`,
return `10`.

# Solution

如果只是用遍历的方法来求解这道题的话，应该还是比较简单的。难度就在于不知道这道题可以用暴力遍历的方式来求解，没有绕过那个弯子。实际上是可以用遍历来求解的，我们可以每个长方形，对于每个长方形，我们遍历求解出，以该长方形为所围成面积的最右面，向前遍历可能的所有情况。

在向前遍历的时候，需要记录下遍历到的最小的高度，因为所围成的面积需要以该最小的高度作为面积的高度，并记录每次遍历得到的矩形的面积。

```java
class Solution {
    public int largestRectangleArea(int[] heights) {
        //boundary condition
        if(heights == null || heights.length == 0){
            return 0;
        }
        //normal condition
        int max = 0;
        for(int i=0; i<heights.length; i++){
            if(i == heights.length-1 || heights[i] > heights[i+1]){
                int minHeight = heights[i];
                for(int j=i; j>=0; j--){
                    minHeight = Math.min(minHeight, heights[j]);
                    max = Math.max(max, minHeight * (i-j+1));
                }
            }
        }
        return max;
    }
}
```

