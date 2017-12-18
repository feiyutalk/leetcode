# 136. Single NumberSum Root to Leaf Numbers

```java
class Solution {
    public int singleNumber(int[] nums) {
        Map<Integer, Integer> map = new HashMap<>();
        for(int num : nums){
            map.put(num, map.getOrDefault(num, 0) + 1);
        }
        for(Map.Entry<Integer, Integer> entry : map.entrySet()){
            if(entry.getValue() == 1) return entry.getKey();
        }
        return -1;
    }
}
```



