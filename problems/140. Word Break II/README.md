# 140. Word Break II

## #1 递归[AC]

```java
class Solution {
    public List<String> wordBreak(String s, List<String> wordDict) {
        List<String> res = new LinkedList<>();
        HashSet<String> set = new HashSet<>(wordDict);
        HashMap<String, List<String>> used = new HashMap<String, List<String>>();
        res = helper(s, set, used);
        return res;
    }
    
    private List<String> helper(String s, HashSet<String> set, HashMap<String, List<String>> used){
        if(used.containsKey(s))
            return used.get(s);
        if(s.length() == 0) return null;
        List<String> res = new LinkedList<String>();
        for(int i=1; i<=s.length(); i++){
            String sub = s.substring(0, i);
            List<String> partRes = null;
            if(set.contains(sub)){
                partRes = helper(s.substring(i), set, used);
                if(partRes == null)
                    res.add(sub);
                else
                    for(String str : partRes)
                        res.add(sub + " " + str);
            }
        }
        used.put(s, res);
        return res;
    }
}
```

