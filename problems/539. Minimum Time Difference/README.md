# 539. Minimum Time Difference

```java
class Solution {
    public int findMinDifference(List<String> timePoints) {
        if(timePoints == null || timePoints.size() == 0)
            return 0;
        int min = Integer.MAX_VALUE;
        for(int i=0; i<timePoints.size()-1; i++){
            for(int j=i+1; j<timePoints.size(); j++){
                int diff = getDiffMin(timePoints.get(i), timePoints.get(j));
                if(diff < min)
                    min = diff;
            }
        }
        return min;
    }
    
    private int getDiffMin(String str1, String str2){
        String[] t1 = str1.split(":");
        String[] t2 = str2.split(":");
        int h1 = Integer.parseInt(t1[0]);
        int m1 = Integer.parseInt(t1[1]);
        int h2 = Integer.parseInt(t2[0]);
        int m2 = Integer.parseInt(t2[1]);
        int diff1 = (((h1 - h2)+24)%24)*60 + (m1 - m2);
        int diff2 = (((h2 - h1)+24)%24)*60 + (m2 - m1);
        if(diff1 < 0)
            return diff2;
        if(diff2 < 0)
            return diff1;
        return Math.min(diff1, diff2);
    }
}
```

```java
class Solution {
    public int findMinDifference(List<String> timePoints) {
        boolean[] mark = new boolean[24 * 60];
        for (String time : timePoints) {
            String[] t = time.split(":");
            int h = Integer.parseInt(t[0]);
            int m = Integer.parseInt(t[1]);
            if (mark[h * 60 + m]) return 0;
            mark[h * 60 + m] = true;
        }
        
        int prev = 0, min = Integer.MAX_VALUE;
        int first = Integer.MAX_VALUE, last = Integer.MIN_VALUE;
        for (int i = 0; i < 24 * 60; i++) {
            if (mark[i]) {
                if (first != Integer.MAX_VALUE) {
                    min = Math.min(min, i - prev);
                }
                first = Math.min(first, i);
                last = Math.max(last, i);
                prev = i;
            }
        }
        
        min = Math.min(min, (24 * 60 - last + first));
        
        return min;
    }
}
```

