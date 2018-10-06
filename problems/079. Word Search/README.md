[TOC]
# #1 借助辅助空间

## 思路

我们遍历矩阵，记录需要被标记为0的行和列，通过`Set`来存储。然后再次遍历矩阵，如果该`cell`的行或者列在`Set`中，就说明该`cell`需要被标记为0。

## 算法

1. 遍历二维数组，如果`matrix[i][j]==0`，则将`i`存放在`rows`中，将`j`存放在`cols`中；
2. 再次遍历二维数组，如果发现`i in rows or j in cols`，则把该`cell`的值设为0。

![](http://p6sh0jwf6.bkt.clouddn.com/2018-10-05-LeetCode%2073.%20Set%20Matrix%20Zeroes%20%20%E8%A7%A3%E6%B3%951.gif)

```java
class Solution {
  public void setZeroes(int[][] matrix) {
    int R = matrix.length;
    int C = matrix[0].length;
    Set<Integer> rows = new HashSet<Integer>();
    Set<Integer> cols = new HashSet<Integer>();

    for (int i = 0; i < R; i++) {
      for (int j = 0; j < C; j++) {
        if (matrix[i][j] == 0) {
          rows.add(i);
          cols.add(j);
        }
      }
    }

    for (int i = 0; i < R; i++) {
      for (int j = 0; j < C; j++) {
        if (rows.contains(i) || cols.contains(j)) {
          matrix[i][j] = 0;
        }
      }
    }
  }
}
```

## 复杂度分析

- 时间复杂度：$O(M\times N)$
- 空间复杂度：$O(M+N)$