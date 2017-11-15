# 278. First Bad Version

# Solution

转化为二分搜索的问题，本质上就是大于等于类型的二分搜索，直接套用模板即可。

```java
/* The isBadVersion API is defined in the parent class VersionControl.
      boolean isBadVersion(int version); */

public class Solution extends VersionControl {
    public int firstBadVersion(int n) {
        if(n<=0) return n;
        int l = 1, r = n;
        while(l < r){
            int mid = l + (r-l)/2;
            if(isBadVersion(mid)){
                r = mid;
            }else{
                l = mid + 1;
            }
        }
        return l;
    }
}
```

