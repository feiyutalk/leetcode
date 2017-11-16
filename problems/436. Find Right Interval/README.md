# 436. Find Right Interval

# Solution

如果没有时间限制的话，这道题目采用二重循环遍历就可以了，尝试着写了基于二重循环的答案提交，结果还是报超时了。。

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
    public int[] findRightInterval(Interval[] intervals) {
        //boundary condition
        if(intervals == null || intervals.length == 0)
            return new int[0];
        int[] result = new int[intervals.length];
        //normal condition
        for(int i=0; i<intervals.length; i++){
            int min = Integer.MAX_VALUE;
            int end = intervals[i].end;
            int index = -1;
            for(int j=0; j<intervals.length; j++){
                if(j == i) continue;
                if(intervals[j].start >= end){
                    if(intervals[j].start < min){
                        min = intervals[j].start;
                        index = j;
                    }
                }
            }
            result[i] = index;
        }
        return result;
    }
}
```

后面，想到可以在将第二重循环的查找改成二分查找，这样可以将时间复杂度降低。所以，在对二重循环的算法进行优化的时候，优先考虑优化内层循环。

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
    public int[] findRightInterval(Interval[] intervals) {
        Map<Integer, Integer> map = new HashMap<>();
        List<Integer> starts = new ArrayList<>();
        for (int i = 0; i < intervals.length; i++) {
            map.put(intervals[i].start, i);
            starts.add(intervals[i].start);
        }

        Collections.sort(starts);
        int[] res = new int[intervals.length];
        for (int i = 0; i < intervals.length; i++) {
            int end = intervals[i].end;
            int start = binarySearch(starts, end);
            if (start < end) {
                res[i] = -1;
            } else {
                res[i] = map.get(start);
            }
        }
        return res;
    }
    
    public int binarySearch(List<Integer> list, int x) {
        int left = 0, right = list.size() - 1;
        while (left < right) {
            int mid = left + (right - left) / 2;
            if (list.get(mid) < x) { 
                left = mid + 1;
            } else {
                right = mid;
            }
        }
        return list.get(left);
    }
}
```

