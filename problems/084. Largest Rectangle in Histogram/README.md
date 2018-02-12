# 084. Largest Rectangle in Histogram 

## Solution 1 暴力求解[TLE]

直方图中可能构成多个矩形，要求解出这些矩形中最大的面积值，那么最简单、最直接的想法就是遍历所有的矩形，然后比较每个矩形的面积值，得出最大值。问题在于这道题目怎么遍历所有的矩形呢？方式就是遍历输入中每个下标对应的矩形，以该矩形为最右侧构成的所有面积。然后求得所有面积中的最大值。依次遍历所有的输入矩形，就可以得到最终的结果，这种做法比较简单，直接，但是提交的时候会超时。

```java
class Solution {
    public int largestRectangleArea(int[] heights) {
        if(heights == null || heights.length == 0)
            return 0;
        int max = 0;
        for(int i=0; i<heights.length; i++){
            int minHeight = heights[i];
            for(int j=i; j>=0; j--){ //底的宽度为 i-j+1
                minHeight = Math.min(minHeight, heights[j]);
                max = Math.max(max, minHeight*(i-j+1)); 
            }
        }
        return max;
    }
}
```

## Solution 2 优化枚举[AC]

我们需要对算法进行优化，减少没必要的搜索开销，仔细思考会发现一个规律。如果`heights[i] > heights[i+1]`，我不需要遍历以`heights[i]`为最右侧所构成的所有矩形，因为以`heights[i+1]`为最右侧所构成的所有矩形肯定会大于前者，因此，我们可以减少很多时间开销。优化后的代码可以被AC。

```java
class Solution {
    public int largestRectangleArea(int[] heights) {
        if(heights == null || heights.length == 0)
            return 0;
        int max = 0;
        for(int i=0; i<heights.length; i++){
            int minHeight = heights[i];
            if(i == heights.length-1 || heights[i] > heights[i+1])
                for(int j=i; j>=0; j--){ //底的宽度为 i-j+1
                    minHeight = Math.min(minHeight, heights[j]);
                    max = Math.max(max, minHeight*(i-j+1)); 
                }
        }
        return max;
    }
}
```

