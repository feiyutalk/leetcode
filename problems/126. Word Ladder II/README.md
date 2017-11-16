# 126. Word Ladder II

# Solution

做这道题目的时候，一开始直接写了广度优先遍历，结果只能得到一个结果，然后改成了深度优先遍历，结果是出来了，但是心里还是觉得会超时，结果还是超时了。其实上，用将题目抽象成图模型然后再通过深度优先遍历来求解已经挺有难度了，但是还是超时了。先附上深度优先遍历的代码:

```java
class Solution {
    private List<List<String>> result = new ArrayList<>();
    private Set<String>set = new HashSet<>();
    class Node{
        String word;
        List<String> path;
        public Node(String word, List<String> path){
            this.word = word;
            this.path = path;
        }
    }
    
    public List<List<String>> findLadders(String beginWord, String endWord, List<String> wordList) {
        //boundary condition
        if(wordList == null || wordList.size() == 0)
            return new ArrayList<List<String>>();
        if(!wordList.contains(endWord))
            return new ArrayList<List<String>>();
        //normal condition
        dfs(new Node(beginWord, new ArrayList<String>(Arrays.asList(new String[]{beginWord}))), endWord, wordList);
        int min = Integer.MAX_VALUE;
        for(List<String> l : result){
            if(l.size() < min){
                min = l.size();
            }
        }
        List<List<String>> finalResult = new ArrayList<>();
        for(List<String> l : result){
            if(l.size() == min)
                finalResult.add(l);
        }
        return finalResult;
    }
    
    private void dfs(Node cur, String endWord, List<String> wordList){
        if(cur.word.equals(endWord)){
             result.add(cur.path);
             return;
        }else{
            for(String neighbor : getNeighbors(cur.word, wordList)){
                if(!set.contains(neighbor)){
                    set.add(neighbor);
                    List<String> temp = new ArrayList<>(cur.path);
                    temp.add(neighbor);
                    dfs(new Node(neighbor, temp), endWord, wordList);
                    set.remove(neighbor);
                }
            }
        }
    }
    
    private List<String> getNeighbors(String cur, List<String> wordList){
        List<String> result = new ArrayList<>();
        for(String word : wordList){
            if(isNear(cur, word))
                result.add(word);
        }
        return result;
    }
    
    private boolean isNear(String first, String second){
        int count = 0;
        for(int i=0; i<first.length(); i++){
            if(first.charAt(i) != second.charAt(i)){
                count++;
                if(count > 1)
                    return false;
            }
        }
        return true;
    }
}
```

但是回头一想，这道题目除了深度优先遍历，似乎没有更好的解决方案了，可能是自己写的有问题？

现在发现，确实是有问题，那么问题在哪里呢？实际上就是在递归的时候呢，又去遍历寻找每个节点的邻居，这样的话，时间复杂度就上去了，怎么修改呢？当然是时空互换了，就是预先把每个节点的邻居都存起来就可以了。稍微做下修改，得到如下的解:

```java
class Solution {
    private List<List<String>> result = new ArrayList<>();
    private Set<String>set = new HashSet<>();
    class Node{
        String word;
        List<String> path;
        public Node(String word, List<String> path){
            this.word = word;
            this.path = path;
        }
    }
    
    public List<List<String>> findLadders(String beginWord, String endWord, List<String> wordList) {
        //boundary condition
        if(wordList == null || wordList.size() == 0)
            return new ArrayList<List<String>>();
        if(!wordList.contains(endWord))
            return new ArrayList<List<String>>();
        
        //normal condition
        Map<String, List<String>> neighbors = new HashMap<>();
        wordList.add(beginWord);
        for(String word : wordList){
            neighbors.put(word, getNeighbors(word, wordList));
        }
        wordList.remove(beginWord);
        
        dfs(new Node(beginWord, new ArrayList<String>(Arrays.asList(new String[]{beginWord}))), endWord, wordList, neighbors);
        
        int min = Integer.MAX_VALUE;
        for(List<String> l : result){
            if(l.size() < min){
                min = l.size();
            }
        }
        List<List<String>> finalResult = new ArrayList<>();
        for(List<String> l : result){
            if(l.size() == min)
                finalResult.add(l);
        }
        return finalResult;
    }
    
    private void dfs(Node cur, String endWord, List<String> wordList, Map<String, List<String>> neighbors){
        if(cur.word.equals(endWord)){
             result.add(cur.path);
             return;
        }else{
            for(String neighbor : neighbors.get(cur.word)){
                if(!set.contains(neighbor)){
                    set.add(neighbor);
                    List<String> temp = new ArrayList<>(cur.path);
                    temp.add(neighbor);
                    dfs(new Node(neighbor, temp), endWord, wordList, neighbors);
                    set.remove(neighbor);
                }
            }
        }
    }
    
    private List<String> getNeighbors(String cur, List<String> wordList){
        List<String> result = new ArrayList<>();
        for(String word : wordList){
            if(isNear(cur, word))
                result.add(word);
        }
        return result;
    }
    
    private boolean isNear(String first, String second){
        int count = 0;
        for(int i=0; i<first.length(); i++){
            if(first.charAt(i) != second.charAt(i)){
                count++;
                if(count > 1)
                    return false;
            }
        }
        return true;
    }
}
```

即使是这样，还是超时，那么如何进一步优化呢，其实深度优先遍历在这个算法中的缺点在于即便当前遍历时已经比最短路径要长了， 算法也不会终止，因为我提前并不知道最短的距离是多少，后面看了discuss，原来是先用bfs求最短的距离，然后用dfs求所有的解。

```java
public List<List<String>> findLadders(String start, String end, List<String> wordList) {
   HashSet<String> dict = new HashSet<String>(wordList);
   List<List<String>> res = new ArrayList<List<String>>();         
   HashMap<String, ArrayList<String>> nodeNeighbors = new HashMap<String, ArrayList<String>>();// Neighbors for every node
   HashMap<String, Integer> distance = new HashMap<String, Integer>();// Distance of every node from the start node
   ArrayList<String> solution = new ArrayList<String>();

   dict.add(start);          
   bfs(start, end, dict, nodeNeighbors, distance);                 
   dfs(start, end, dict, nodeNeighbors, distance, solution, res);   
   return res;
}

// BFS: Trace every node's distance from the start node (level by level).
private void bfs(String start, String end, Set<String> dict, HashMap<String, ArrayList<String>> nodeNeighbors, HashMap<String, Integer> distance) {
  for (String str : dict)
      nodeNeighbors.put(str, new ArrayList<String>());

  Queue<String> queue = new LinkedList<String>();
  queue.offer(start);
  distance.put(start, 0);

  while (!queue.isEmpty()) {
      int count = queue.size();
      boolean foundEnd = false;
      for (int i = 0; i < count; i++) {
          String cur = queue.poll();
          int curDistance = distance.get(cur);                
          ArrayList<String> neighbors = getNeighbors(cur, dict);

          for (String neighbor : neighbors) {
              nodeNeighbors.get(cur).add(neighbor);
              if (!distance.containsKey(neighbor)) {// Check if visited
                  distance.put(neighbor, curDistance + 1);
                  if (end.equals(neighbor))// Found the shortest path
                      foundEnd = true;
                  else
                      queue.offer(neighbor);
                  }
              }
          }

          if (foundEnd)
              break;
      }
  }

// Find all next level nodes.    
private ArrayList<String> getNeighbors(String node, Set<String> dict) {
  ArrayList<String> res = new ArrayList<String>();
  char chs[] = node.toCharArray();

  for (char ch ='a'; ch <= 'z'; ch++) {
      for (int i = 0; i < chs.length; i++) {
          if (chs[i] == ch) continue;
          char old_ch = chs[i];
          chs[i] = ch;
          if (dict.contains(String.valueOf(chs))) {
              res.add(String.valueOf(chs));
          }
          chs[i] = old_ch;
      }

  }
  return res;
}

// DFS: output all paths with the shortest distance.
private void dfs(String cur, String end, Set<String> dict, HashMap<String, ArrayList<String>> nodeNeighbors, HashMap<String, Integer> distance, ArrayList<String> solution, List<List<String>> res) {
    solution.add(cur);
    if (end.equals(cur)) {
       res.add(new ArrayList<String>(solution));
    } else {
       for (String next : nodeNeighbors.get(cur)) {            
            if (distance.get(next) == distance.get(cur) + 1) {
                 dfs(next, end, dict, nodeNeighbors, distance, solution, res);
            }
        }
    }           
   solution.remove(solution.size() - 1);
}
```

