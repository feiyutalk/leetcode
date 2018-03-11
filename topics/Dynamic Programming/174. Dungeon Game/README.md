# 174. Dungeon Game

# #1 动态规划[AC]

题目中规定只能往下和右两个方向走，也不能回头走，这是符合动态规划状态转化特点的，动态规划的特点在于用已知来推未知，状态转化的方式是固定的，这个方向就是从未知的结果->已知结果 推导的方向，做动态规划的题目，需要定义好状态，紧接着是状态转化的方程，一开始就这种题目确实比较费劲，做多的就习惯了，这道题目的状态就是进入每个dungeon时最少需要的血量，我们要知道的是初始的血量，我们已知的到达最后未知的时候，最少需要的血量是Math.max(1-dungeon[m-1][n-1， 1)，我们从最后一个位置开始向第一个位置推导，这就是我们未知推已知的过程，这个推导公式怎么写，就是我们的状态转移方程。

```java
class Solution {
    public int calculateMinimumHP(int[][] dungeon) {
        //boundary condition
        if(dungeon == null || dungeon.length == 0 || dungeon[0].length == 0)
            return 0;
        //normal condition
        int m = dungeon.length;
        int n = dungeon[0].length;
        int[][] hp = new int[m][n];
        hp[m-1][n-1] = Math.max(1-dungeon[m-1][n-1], 1);
        //last column
        for(int i=m-2; i>=0; i--){
            hp[i][n-1] = Math.max(1, hp[i+1][n-1] - dungeon[i][n-1]);
        }
        //last row
        for(int j=n-2; j>=0; j--){
            hp[m-1][j] = Math.max(1, hp[m-1][j+1] - dungeon[m-1][j]);
        }
        // dp
        for(int i=m-2; i>=0; i--){
            for(int j=n-2; j>=0; j--){
                int right = Math.max(hp[i][j+1] - dungeon[i][j], 1);
                int down = Math.max(hp[i+1][j] - dungeon[i][j], 1);
                hp[i][j] = Math.min(right, down);
            }
        }
        
        return hp[0][0];
    }
}
```

