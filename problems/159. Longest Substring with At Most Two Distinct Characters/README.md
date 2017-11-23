# 159. Longest Substring with At Most Two Distinct Characters

这是`Two Points`的窗口类问题，我们需要保持窗口中只有两个不同的元素，所以我们需要统计当前窗口中每个元素出现的次数，然后再移动第二个指针的时候，判断当前窗口的状态，如果破坏的窗口状态，就需要移动head来并保持窗口的状态。

```java
class Solution {
    public int lengthOfLongestSubstringTwoDistinct(String s) {
        if(s == null || s.length() == 0)
            return 0;
        int res = 0;
        int head = 0;
        Map<Character, Integer> map = new HashMap<>();
        
        for(int i=0; i<s.length(); i++){
            map.put(s.charAt(i), map.getOrDefault(s.charAt(i), 0)+1);
            while(map.size() > 2){
                map.put(s.charAt(head), map.get(s.charAt(head))-1);
                if(map.get(s.charAt(head)) == 0)
                    map.remove(s.charAt(head));
                head += 1;
            }
            res = Math.max(res, i-head+1);
        }
        return res;
    }
}
```

