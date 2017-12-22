# 346. Moving Average from Data Stream

```java
class MovingAverage {
    private int size;
    private int idx = -1;
    List<Integer> arr;
    /** Initialize your data structure here. */
    public MovingAverage(int size) {
        this.size = size;
        arr = new ArrayList<>();
    }
    
    public double next(int val) {
        idx++;
        arr.add(val);
        double res = 0;
        int count = 0;
        for(int i=idx; i>idx-size && i>=0; i--){
            res += arr.get(i);
            count++;
        }
        return res/count;
    }
}

/**
 * Your MovingAverage object will be instantiated and called as such:
 * MovingAverage obj = new MovingAverage(size);
 * double param_1 = obj.next(val);
 */
```

