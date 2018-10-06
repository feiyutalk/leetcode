# #1 DFS[ac]

## 思路

以每个`cell`为深度搜索的起始点，采用dfs的方式遍历每个一种可能路径，若存在一种路径的字符序列与`word`相同，则返回`true`，否则返回`false`。

## 算法

![](http://p6sh0jwf6.bkt.clouddn.com/2018-10-06-LeetCode%2079.%20Word%20Search%20dfs%E8%A7%A3%E6%B3%95.gif)

```java
class Solution {
    int[][] dirs = {{-1, 0}, {1,0}, {0, -1}, {0, 1}};
    boolean[][] used;
    int m;
    int n;
    public boolean exist(char[][] board, String word) {
        if(board == null || board.length == 0 || board[0] == null || board[0].length == 0) return false;
        if(word == null || word.length() == 0) return false;
        m = board.length;
        n = board[0].length;
        for(int i=0; i<m; i++){
            for(int j=0; j<n; j++){
                used = new boolean[m][n];
                if(dfs(board, word, 0, i, j))
                    return true;
            }
        }
        return false;
    }
    
    public boolean dfs(char[][] board, String word, int step, int row, int col){
        if(word.charAt(step) != board[row][col])
            return false;
        if(step == word.length()-1) 
            return true;
        used[row][col] = true;
        for(int[] dir : dirs){
            int r = row + dir[0];
            int c = col + dir[1];
            if(r < 0 || r >= m || c < 0 || c >= n || used[r][c]) continue;
            if(dfs(board, word, step+1, r, c))
                return true;
        }
        used[row][col] = false;
        return false;
    }
}
```

## 复杂度分析

- 时间复杂度：