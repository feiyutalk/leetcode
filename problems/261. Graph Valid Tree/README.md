# 261. Graph Valid Tree

```java
class Solution {
    public boolean validTree(int n, int[][] edges) {
        if(n != edges.length+1)
            return false;
        if(edges.length == 0){
            if(n == 1) return true;
            else return false;
        }
        boolean[] visited = new boolean[n];
        return helper(edges[0][0], edges, visited) && allVisited(visited);
    }
    
    private boolean helper(int cur, int[][] edges, boolean[] visited){
        if(visited[cur]){
            return false;
        }
        visited[cur] = true;
        for(int next : getNexts(cur, edges, visited)){
            if(helper(next, edges, visited) == false) return false;
        }
        return true;
    }
    
    private List<Integer> getNexts(int cur, int[][] edges, boolean[] visited){
        Set<Integer> res = new HashSet<>();
        for(int[] edge : edges){
            if(edge[0] == cur && !visited[edge[1]])
                res.add(edge[1]);
        }
        for(int[] edge : edges){
            if(edge[1] == cur && !visited[edge[0]])
                res.add(edge[0]);
        }
        return new ArrayList<Integer>(res);
    }
    
    private boolean allVisited(boolean[] visited){
        for(boolean v : visited)
            if(v == false)
                return false;
        return true;
    }
}
```

