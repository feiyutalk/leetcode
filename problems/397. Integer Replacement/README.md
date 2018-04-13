# 397. Integer Replacement

## #1 BFS[AC]

### 思路

把每个数字看做图中的一个节点，两个节点之间是否有边相连，通过`n %2 == 0 -> n/2`和`n % 2 != 0-> n+1, n-1`这个条件来判断，这样就把问题看做是一个图。最后，通过广度优先遍历找到最近的路径。

![Screen Shot 2018-04-13 at 11.05.31](../../../../../../../Desktop/Screen Shot 2018-04-13 at 11.05.31.png)

### 算法

```java
class Solution {
    public int integerReplacement(int n) {
        assert n > 0;
        Queue<Long> queue = new LinkedList<>();
        queue.offer((long)n);
        return bfs(queue, 0);
    }
    
    private int bfs(Queue<Long> oldqueue, int level) {
        Queue<Long> newqueue = new LinkedList<>();
        while (!oldqueue.isEmpty()) {
            long n = oldqueue.poll();
            if (n == 1) {
                return level;
            }
            if (n % 2 == 0) {
                newqueue.offer(n / 2);
            } else {
                newqueue.offer(n + 1);
                newqueue.offer(n - 1);
            }
        }
        return bfs(newqueue, level + 1);
    }
}
```

上面例子的执行方式如下所示：

![Screen Shot 2018-04-13 at 11.07.08](../../../../../../../Desktop/Screen Shot 2018-04-13 at 11.07.08.png)

### 复杂度分析：

- ？
- 空间复杂度：$O(logn)$

## #2 位操作[AC]

### 算法

```java
public int integerReplacement(int n) {
    int c = 0;
    while (n != 1) {
        if ((n & 1) == 0) {
            n >>>= 1;
        } else if (n == 3 || Integer.bitCount(n + 1) > Integer.bitCount(n - 1)) {
            --n;
        } else {
            ++n;
        }
        ++c;
    }
    return c;
}
```

