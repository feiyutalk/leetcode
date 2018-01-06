# 452. Minimum Number of Arrows to Burst Balloons

```java
class Solution {
    public int findMinArrowShots(int[][] points) {
        if(points == null || points.length == 0)
            return 0;
        Arrays.sort(points,(a, b)->a[1]-b[1]);
        int count = 1;
        int pos = points[0][1];
        for(int i=0; i<points.length; i++){
            if(pos >= points[i][0]) continue;
            count++;
            pos = points[i][1];
        }
        return count;
    }
}
```

