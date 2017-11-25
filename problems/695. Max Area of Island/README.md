# 695. Max Area of Island

将二维数组抽象成一个图结构，该图有多个子图，我们去遍历每个子图，所有子图中结点数最多的子图就是所要求的Max Area。

对子图的遍历可以采用深度优先也可以采用广度优先，应该先考虑深度优先，因为其代码比较简单。

```java
class Solution {
    public int maxAreaOfIsland(int[][] grid) {
        if(grid == null || grid.length == 0)
            return 0;
        int m = grid.length;
        int n = grid[0].length;
        int max = 0;
        for(int i=0; i<m; i++){
            for(int j=0; j<n; j++){
                if(grid[i][j] == 1){
                    int area = dfs(grid, i, j, m, n, 0);
                    max = Math.max(area, max);
                }
            }
        }
        return max;
    }
    
    private int dfs(int[][] grid, int i, int j, int m, int n, int area){
        if(i < 0 || i >= m || j < 0 || j >=n || grid[i][j] == 0){
            return area;
        }
        grid[i][j] = 0;
        area++;
        area = dfs(grid, i+1, j, m, n, area);
        area = dfs(grid, i-1, j, m, n, area);
        area = dfs(grid, i, j+1, m, n, area);
        area = dfs(grid, i, j-1, m, n, area);
        return area;
    }
}
```

