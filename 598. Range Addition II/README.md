# 598. Range Addition II 

# Solution

这道题目充分体现抓住问题的主要矛盾的重要性，忽略次要矛盾，抓住主要矛盾，只要这样才能在面对新的问题时，通过已有的知识进行总结。因为，在面对新的问题的时候，问题的背景，表面信息往往都是我们没见过的，但是问题的本质算法，本质解法一定是我们已经总结过的。如何抓住问题的主要矛盾（本质算法），而忽略次要矛盾（背景及表面信息）很大程度上决定了我们做算法题目的正确率和速度。但是，这必须建立在对已做过题目的大量总结的基础上。

那这道题目的主要矛盾在哪里呢？

> 这道题目，说了那么多，实际上问的就是以（0，0）作为左顶点，长和宽任意（通过ops输入）的多组矩形的相交矩形的面积是多少。

其实，相交的矩形面积就是等于所有矩形中长最小值，和所有矩形中宽最小值的乘积。

```java
class Solution {
    public int maxCount(int m, int n, int[][] ops) {
        //boundary condition
        if(m <=0 || n <= 0)
            return 0;
        if(ops == null || ops.length == 0)
            return m*n;
        //normal condition
        int minRow = Integer.MAX_VALUE;
        int minCol = Integer.MAX_VALUE;
        for(int[] op : ops){
            if(op[0] < minRow) minRow = op[0];
            if(op[1] < minCol) minCol = op[1];
        }
        return minRow * minCol;
    }
}
```

