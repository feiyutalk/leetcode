# 200. Number of Islands

```java
class Solution {
    class Cell{
        int r;
        int c;
        public Cell(int r, int c){
            this.r = r;
            this.c = c;
        }
    }
    public int numIslands(char[][] grid) {
        if(grid == null || grid.length == 0)
            return 0;
        int[][] dirs  = {{1,0},{0,1},{-1,0},{0,-1}};
        int res = 0;
        int m = grid.length;
        int n = grid[0].length;
        for(int i=0; i<m; i++){
            for(int j=0; j<n; j++){
                if(grid[i][j] == 0)
                    continue;
                res++;
                Queue<Cell> queue = new LinkedList<>();
                queue.offer(new Cell(i, j));
                while(!queue.isEmpty()){
                   Cell cur = queue.poll();
                   for(int[] dir : dirs){
                        int r = cur.r + dir[0];
                        int c = cur.c + dir[1];
                        if(r<0 || r>=m || c<0 || c>=n || grid[r][c] == 0)
                            continue;
                        grid[r][c] = 0;
                        queue.offer(new Cell(r, c));
                   }     
                }
            }
        }
        return res;
    }
}
```

