# 463. Island Perimeter

```java
class Solution {
    public int islandPerimeter(int[][] grid) {
        int res = 0;
        int m = grid.length;
        int n = grid[0].length;
        for(int i=0; i<m; i++){
            for(int j=0; j<n; j++){
                if(grid[i][j] == 1){
                    //left
                    if(j==0 || grid[i][j-1]==0) res++;
                    // up
                    if(i==0 || grid[i-1][j]==0) res++;
                    //right
                    if(j==n-1 || grid[i][j+1]==0) res++;
                    //down
                    if(i==m-1 || grid[i+1][j]==0) res++;
                }
            }
        }
        return res;
    }
}
```

