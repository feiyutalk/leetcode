# 240. Search a 2D Matrix II

# Solution

这是一道搜索的题目，搜索类的题目最常见的就是二分搜索，但是这道题目比较特别，我们发现如果从最右上角元素开始进行搜索，如果比target小的往下走，如果比target大就往左走，这样的话，最后是能够得出结果的。

```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        if(matrix == null || matrix.length == 0) return false;
        int m = matrix.length;
        int n = matrix[0].length;
        for(int i=0, j=n-1; i<m && j>=0;){
            if(matrix[i][j] == target) return true;
            else if(matrix[i][j] > target) j--;
            else i++;
        }
        return false;
    }
}
```

