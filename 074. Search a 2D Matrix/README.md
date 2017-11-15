# 074. Search a 2D Matrix

# Solution

这道题目，本质上还是二分搜索的问题，只是将我们之前二分问题中常见的一维数组经拓展，变成了二维数组。做法还是一样的，根据二分的模板来做。只是在判断的时候，需要获得对应序列所在的行和列，然后得到该值。

```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        if(matrix == null || matrix.length == 0) return false;
        int m = matrix.length;
        int n = matrix[0].length;
        int l = 0, r = m*n - 1;
        while(l<=r){
            int mid = l + (r-l)/2;
            int row = mid/n;
            int col = mid%n;
            if(matrix[row][col] == target) return true;
            else if(matrix[row][col] < target) l = mid+1;
            else r = mid-1;
        }
        return false;
    }
}
```

