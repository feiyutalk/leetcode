# 397. Integer Replacement

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

