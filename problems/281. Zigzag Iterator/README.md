# 281. Zigzag Iterator

```java
public class ZigzagIterator {
    private List<Integer> r = new ArrayList<>();
    private int idx = 0;
    public ZigzagIterator(List<Integer> v1, List<Integer> v2) {
        int i=0;
        for(;i<v1.size()&&i<v2.size();i++){
            r.add(v1.get(i));
            r.add(v2.get(i));
        }
        while(i<v1.size()){
            r.add(v1.get(i++));
        }
        while(i<v2.size()){
            r.add(v2.get(i++));
        }
    }

    public int next() {
        return r.get(idx++);
    }

    public boolean hasNext() {
        return idx != r.size();
    }
}

/**
 * Your ZigzagIterator object will be instantiated and called as such:
 * ZigzagIterator i = new ZigzagIterator(v1, v2);
 * while (i.hasNext()) v[f()] = i.next();
 */
```

