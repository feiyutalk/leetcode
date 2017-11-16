# 274. H-Index

# Solution

这个问题本质上还是一个搜索问题，我们可以转化为二分的模板来求解，但是这个转化会有点绕，导致这个问题的难度比较高。我们需要先对数组进行排序(只是进行二分搜索必须要的)，然后直接套用二分算法的模板就可以了，这边的比较条件是根据题目的意思进行修改的。

```java
class Solution {
    public int hIndex(int[] citations) {
        if(citations == null || citations.length == 0) return 0;
        Arrays.sort(citations);
        int n = citations.length;
        int l = 0, r = citations.length-1;
        while(l<=r){
            int mid = l + (r - l)/2;
            if(citations[mid] == n - mid) return citations[mid];
            else if(citations[mid] < n - mid) l = mid + 1;
            else r = mid - 1;
        }
        return n-l;
    }
}
```

