# 630. Course Schedule III

## #1 动态规划[TLE]

```java
public class Solution {
    public int scheduleCourse(int[][] courses) {
        Arrays.sort(courses, (a, b) -> a[1] - b[1]);
        Integer[][] memo = new Integer[courses.length][courses[courses.length - 1][1] + 1];
        return schedule(courses, 0, 0, memo);
    }
    public int schedule(int[][] courses, int i, int time, Integer[][] memo) {
        if (i == courses.length)
            return 0;
        if (memo[i][time] != null)
            return memo[i][time];
        int taken = 0;
        if (time + courses[i][0] <= courses[i][1])
            taken = 1 + schedule(courses, i + 1, time + courses[i][0], memo);
        int not_taken = schedule(courses, i + 1, time, memo);
        memo[i][time] = Math.max(taken, not_taken);
        return memo[i][time];
    }
}
```

## #2 贪心[AC]

```java

public class Solution {
    public int scheduleCourse(int[][] courses) {
        Arrays.sort(courses, (a, b) -> a[1] - b[1]);
        int time = 0, count = 0;
        for (int i = 0; i < courses.length; i++) {
            if (time + courses[i][0] <= courses[i][1]) {
                time += courses[i][0];
                courses[count++] = courses[i];
            } else {
                int max_i = i;
                for (int j = 0; j < count; j++) {
                    if (courses[j][0] > courses[max_i][0])
                        max_i = j;
                }
                if (courses[max_i][0] > courses[i][0]) {
                    time += courses[i][0] - courses[max_i][0];
                    courses[max_i] = courses[i];
                }
            }
        }
        return count;
    }
}
```

