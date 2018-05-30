# 332. Reconstruct Itinerary

## #1 DFS[AC]

这道题目可以用深度优先遍历来搜索，首先需要记录每个机场的所有可达机场，可以通过 `Map<String, List<String>> map`来存储，需要记住的是，我们需要对所有可达机场进行排序，以保证按照序列最小的选择顺序进行选择。然后，我们从`"JFK"`这个机场开始深度搜索。

```java
class Solution {
    List<String> res = new ArrayList<>();
    public List<String> findItinerary(String[][] tickets) {
        if(tickets == null || tickets.length == 0)
            return new ArrayList<String>();
        // 获得所有的邻居
        Map<String, List<String>> map = new HashMap<>();
        for(int i=0; i<tickets.length; i++){
            if(!map.containsKey(tickets[i][0])){
                List<String> temp = new ArrayList<>();
                temp.add(tickets[i][1]);
                map.put(tickets[i][0], temp);
            }else{
                List<String> temp  = map.get(tickets[i][0]);
                temp.add(tickets[i][1]);
                // 排序
                Collections.sort(temp);
                map.put(tickets[i][0], temp);
            }
        }
        res.add("JFK");
        robot(tickets, map, "JFK", 0);
        return res;
    }
    
    public boolean robot(String[][] tickets, Map<String, List<String>> map, 
                      String cur,int count){
        if(count == tickets.length)
            return true;
        //System.out.println(cur);
        List<String> nexts = map.get(cur);//获得邻居
        //System.out.println(cur + ":" + nexts);
        if(nexts == null || nexts.size() == 0){
            return false;
        }
        for(int i=0; i<nexts.size(); i++){
            String next = nexts.get(i);
            res.add(next);
            nexts.remove(i);
            map.put(cur, nexts);
            if(robot(tickets, map, next, count+1))
                return true;
            res.remove(res.size()-1);
            nexts.add(i, next);
        }
        return false;
    }
}
```

