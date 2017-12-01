# 323. Number of Connected Components in an Undirected Graph

```java
class Solution {
    public int countComponents(int n, int[][] edges) {
        if(n <= 1)
            return n;
        if(edges == null || edges.length == 0) // no edges
            return n;
        Map<Integer, List<Integer>> neighbors = new HashMap<>();
        for(int i=0; i<n; i++)
            neighbors.put(i, new ArrayList<Integer>());
        for(int[] edge : edges){
            List<Integer> neighbor = neighbors.get(edge[0]);
            neighbor.add(edge[1]);
            
            List<Integer> neighbor2 = neighbors.get(edge[1]);
            neighbor2.add(edge[0]);
        }
        int res = 0;
        boolean[] visited = new boolean[n];
        for(int i=0; i<n; i++){
            if(!visited[i]){
                res++;
                Queue<Integer> queue = new LinkedList<>();
                queue.offer(i);
                while(!queue.isEmpty()){
                    int cur = queue.poll();
                    visited[cur] = true;
                    for(int next : neighbors.get(cur)){
                        if(!visited[next])
                            queue.offer(next);
                    }
                }
            }
        }
        return res;
    }
}
```

