# 361. Bomb Enemy

```java
class Solution {
    public int maxKilledEnemies(char[][] grid) {
        if(grid == null || grid.length == 0 || grid[0].length == 0) return 0;
        int m = grid.length;
        int n = grid[0].length;
        int[][] count = new int[m][n];
        int res = 0;
        //col : left -> right
        for(int i=0; i<m; i++){
            int tmp = 0;
            for(int j=0; j<n; j++){
                if(grid[i][j] == 'W') tmp = 0;
                else if(grid[i][j] == 'E') tmp += 1;
                else if(grid[i][j] == '0') {
                    count[i][j] = tmp;
                    res = Math.max(res, count[i][j]);
                }
            }
            tmp = 0;
            for(int j=n-1; j>=0; j--){
                if(grid[i][j] == 'W') tmp = 0;
                else if(grid[i][j] == 'E') tmp += 1;
                else if(grid[i][j] == '0') {
                    count[i][j] += tmp;
                    res = Math.max(res, count[i][j]);
                }
            }
        }
        //row : top -> down
        for(int j=0; j<n; j++){
            int tmp = 0;
            for(int i=0; i<m; i++){
                if(grid[i][j] == 'W') tmp = 0;
                else if(grid[i][j] == 'E') tmp += 1;
                else if(grid[i][j] == '0'){
                    count[i][j] += tmp;
                    res = Math.max(res, count[i][j]);
                }
            }
            tmp = 0;
            for(int i=m-1; i>=0; i--){
                if(grid[i][j] == 'W') tmp = 0;
                else if(grid[i][j] == 'E') tmp += 1;
                else if(grid[i][j] == '0'){
                    count[i][j] += tmp;
                    res = Math.max(res, count[i][j]);
                }
            }
        }
        return res;
    }
}
```

