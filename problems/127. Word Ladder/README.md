# 127. Word Ladder 

```java
class Solution {
    class Node{
        String s;
        int step;
        public Node(String s, int step){
            this.s = s;
            this.step = step;
        }
    }
    public int ladderLength(String beginWord, String endWord, List<String> wordList) {
        if(wordList == null || wordList.size() == 0 || !wordList.contains(endWord))
            return 0;
        // init neighbors
        Map<String, List<String>> neighbors = new HashMap<>();
        // init begin word
        neighbors.put(beginWord, getNeighbors(beginWord, wordList));
        // init other word
        for(String w : wordList){
            neighbors.put(w, getNeighbors(w, wordList));
        }
        // bfs
        Queue<Node> queue = new LinkedList<>();
        Set<String> set = new HashSet<>();
        queue.offer(new Node(beginWord, 1));
        set.add(beginWord);
        while(!queue.isEmpty()){
            Node cur = queue.poll();
            for(String nei : neighbors.get(cur.s)){
                if(!set.contains(nei)){
                    if(nei.equals(endWord)) return cur.step+1;
                    queue.offer(new Node(nei, cur.step+1));
                    set.add(nei);
                }
            }
        }
        return 0;
    }
    
    private List<String> getNeighbors(String word, List<String> wordList){
        List<String> res = new ArrayList<>();
        for(String w : wordList){
            int count = 0;
            for(int i=0; i<w.length(); i++){
                if(word.charAt(i) != w.charAt(i)){
                    count++;
                    if(count>1)
                        break;
                }
            }
            if(count == 1)
                res.add(w);
        }
        return res;
    }
}
```

