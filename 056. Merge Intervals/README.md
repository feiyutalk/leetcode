# Merge Intervals

# Description

Given a collection of intervals, merge all overlapping intervals.

For example,
Given `[1,3],[2,6],[8,10],[15,18]`,
return `[1,6],[8,10],[15,18]`.

# Solution

这道题目意思非常清楚，就是需要合并有重合的区间，最后返回所有不重合的区间。一个比较直接的想法就是先对集合进行排序，按照区间的开始来排序，这样之后我们再对这个区间进行遍历，我们可以通过两个变量来记录住上一个区间的start和end，然后当前的这个区间的start和end与上一个区间的start和end进行比较，比较的基本做法就是当前区间的start是否小于等于上一个区间的end，如果是的话，就把它并入到上一个区间，这边只需要修改上一个区间的end即可。当然，有可能当前的start大于上一个区间的end，这样的话，上一个区间就算是完成了，可以单独作为一个区间存在，这时候就可以把它加入到结果数组中。

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
    public List<Interval> merge(List<Interval> intervals) {
        //boundary condition
        if(intervals == null || intervals.size() <=1)
            return intervals;
        //normal condition
        // step 1 sort the list
        intervals.sort((i1, i2) -> (Integer.compare(i1.start, i2.start)));
        // step 2 loop the list
        List<Interval> result = new ArrayList<Interval>();
        int start = intervals.get(0).start;
        int end = intervals.get(0).end;
        for(Interval interval : intervals){
            if(interval.start <= end){
                end = Math.max(end, interval.end);
            }else{
                result.add(new Interval(start, end));
                start = interval.start;
                end = interval.end;
            }
        }
        result.add(new Interval(start, end));
        return result;
    }
}
```

---

**enjoy life, coding now! :D**