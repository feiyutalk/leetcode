# 529. Minesweeper
## Description

```
Difficulty: Medium
```

You are given a 2D char matrix representing the game board. 'M' represents an unrevealed mine, 'E' represents an unrevealed empty square, 'B' represents a revealed blank square that has no adjacent (above, below, left, right, and all 4 diagonals) mines, digit ('1' to '8') represents how many mines are adjacent to this revealed square, and finally 'X' represents a revealed mine.

Now given the next click position (row and column indices) among all the unrevealed squares ('M' or 'E'), return the board after revealing this position according to the following rules:

1. If a mine ('M') is revealed, then the game is over - change it to 'X'.
2. If an empty square ('E') with no adjacent mines is revealed, then change it to revealed blank ('B') and all of its adjacent unrevealed squares should be revealed recursively.
3. If an empty square ('E') with at least one adjacent mine is revealed, then change it to a digit ('1' to '8') representing the number of adjacent mines.
4. Return the board when no more squares will be revealed.

**Example 1:**

```

Input: 

[['E', 'E', 'E', 'E', 'E'],
 ['E', 'E', 'M', 'E', 'E'],
 ['E', 'E', 'E', 'E', 'E'],
 ['E', 'E', 'E', 'E', 'E']]

Click : [3,0]

Output: 

[['B', '1', 'E', '1', 'B'],
 ['B', '1', 'M', '1', 'B'],
 ['B', '1', '1', '1', 'B'],
 ['B', 'B', 'B', 'B', 'B']]

```
## Solution 1
  这道题目本质是一个图的遍历问题，二维数组中的元素可以映射为图中的节点，矩阵中元素的相邻关系，可以映射成图中节点是否有连线。那我们需要去遍历图中的节点，并根据题目的要求来进行相应的操作，也就是在遍历的过程中添加操作因子：

1. 如果该元素的值为'M',则将其该为'X'，游戏结束，不再往下遍历。
2. 首先应该先获得周围地雷的个数，如果个数为0；则把该元素的值改为'B',继续递归遍历。如果个数大于0，说明周围有地雷，把该值改为地雷的个数，不再继续遍历。

```java

class Solution {
    public char[][] updateBoard(char[][] board, int[] click) {
        dfs(board, click);
        return board;
    }
    
    // graph model dfs
    public void dfs(char[][] board, int[] click){
        int row = click[0];
        int col = click[1];
        int m = board.length;
        int n = board[0].length;
        if(board[row][col] == 'M'){
            board[row][col] = 'X';
        }else{
            //get the number of adjacent mines
            int count = 0;
            for(int i=-1;i<2;i++){
                for(int j=-1;j<2;j++){
                    int r = row + i;
                    int c = col + j;
                    if(i == 0 && j == 0)
                        continue;
                    if(r<0 || r>=m || c < 0 || c >= n)
                        continue;
                    if(board[r][c] == 'M' || board[r][c] == 'X')
                        count++;
                }
            }
            if(count > 0){//need not dfs
                board[row][col] = (char)(count+'0');
            }else{
                board[row][col] = 'B';
                //dfs
                for(int i=-1;i<2;i++){
                    for(int j=-1;j<2;j++){
                        int r = row + i;
                        int c = col + j;
                        if(i == 0 && j == 0)
                            continue;
                        if(r<0 || r>=m || c < 0 || c >= n)
                            continue;
                        if(board[r][c] == 'E')
                            dfs(board, new int[]{r,c});
                    }
                }
            }
        }
    }
}
```

***

**enjoy life, coding now! :D**
