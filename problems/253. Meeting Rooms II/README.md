# 253. Meeting Rooms II

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
    public int minMeetingRooms(Interval[] intervals) {
        if(intervals == null || intervals.length == 0)
            return 0;
        Arrays.sort(intervals, new Comparator<Interval>(){
            public int compare(Interval v1, Interval v2){
                return v1.start - v2.start;
            }
        });
        PriorityQueue<Interval> heap = new PriorityQueue<Interval>(intervals.length, new Comparator<Interval>(){
            public int compare(Interval v1, Interval v2){
                return v1.end - v2.end;
            }
        });
        heap.offer(intervals[0]);
        for(int i=1; i<intervals.length; i++){
            Interval cur = heap.poll();
            if(intervals[i].start >= cur.end){
                cur.end = intervals[i].end;
            }else{
                heap.offer(intervals[i]);
            }
            heap.offer(cur);
        }
        return heap.size();
    }
}
```





