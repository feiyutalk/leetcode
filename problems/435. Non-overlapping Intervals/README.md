# 435. Non-overlapping Intervals

## #1 贪心[AC]

```java
/**
 * Definition for an interval.
 * public class Interval {
 *     int start;
 *     int end;
 *     Interval() { start = 0; end = 0; }
 *     Interval(int s, int e) { start = s; end = e; }
 * }
 */
class Solution {
    public int eraseOverlapIntervals(Interval[] intervals) {
        if(intervals == null || intervals.length == 0)
            return 0;
        Arrays.sort(intervals, new Comparator<Interval>(){
           public int compare(Interval a, Interval b){
               return a.end - b.end;
           } 
        });
        int res = 0;
        int lastEnd = intervals[0].end;
        for(int i=1; i<intervals.length; i++){
            if(intervals[i].start < lastEnd)
                res++;
            else{
                lastEnd = intervals[i].end;
            }
        }
        return res;
    }
}
```

