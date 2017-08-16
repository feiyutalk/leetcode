# 433. Minimum Genetic Mutation
## Description

```
Difficulty: Medium
```

A gene string can be represented by an 8-character long string, with choices from "A", "C", "G", "T".

Suppose we need to investigate about a mutation (mutation from "start" to "end"), where ONE mutation is defined as ONE single character changed in the gene string.

For example, "AACCGGTT" -> "AACCGGTA" is 1 mutation.

Also, there is a given gene "bank", which records all the valid gene mutations. A gene must be in the bank to make it a valid gene string.

Now, given 3 things - start, end, bank, your task is to determine what is the minimum number of mutations needed to mutate from "start" to "end". If there is no such a mutation, return -1.

**Note:**

1. Starting point is assumed to be valid, so it might not be included in the bank.

2. If multiple mutations are needed, all mutations during in the sequence must be valid.

3. You may assume start and end string is not the same.

**Example 1:**

    start: "AACCGGTT"
    end:   "AACCGGTA"
    bank: ["AACCGGTA"]
	
	return: 1

**Example 2:**

    start: "AACCGGTT"
    end:   "AAACGGTA"
    bank: ["AACCGGTA", "AACCGCTA", "AAACGGTA"]
	
	return: 2
**Example 3:**

	start: "AAAAACCC"
	end:   "AACCCCCC"
	bank: ["AAAACCCC", "AAACCCCC", "AACCCCCC"]

	return: 3


## Solution 1
  其实上在分析、解决问题的时候，我们需要抓住问题的本质！然后把这些相同的问题的本质抽象出来！线性表、树、图等等。这些模型都是抽象的，它不针对具体的应用，但是却能够满足该和该模型本质相同的所有应用！

	public class Solution {
	    public int count = 0;
	    public boolean find = false;
	    public int minMutation(String start, String end, String[] bank) {
	        boolean exist = false;
	        for(String s : bank){
	            if(end.equals(s))
	                exist = true;
	        }
	        if(!exist)
	            return -1;
	        
	        HashMap<String, Boolean> visited = new HashMap<>();
	        for(String s : bank){
	            visited.put(s, false);
	        }
	        
	        Queue<NodeInfo> queue = new LinkedList<>();
	        queue.offer(new NodeInfo(start, 0));
	        widthSearch(queue,end,bank,visited);
	        if(!visited.get(end))
	            return -1;
	        return count;
	    }
	    
	    public void widthSearch(Queue<NodeInfo> queue, String end, String[] bank, HashMap<String, Boolean> visited){
	        if(queue.size() == 0 || find)
	            return;
	        NodeInfo cur = queue.poll();
	        for(String neighbor : findNeighbors(cur.s, bank)){
	            if(!visited.get(neighbor)){
	                visited.put(neighbor,true);
	                if(neighbor.equals(end)){
	                    find = true;
	                    break;
	                }else{
	                    queue.offer(new NodeInfo(neighbor, cur.level+1));
	                }
	            }
	        }
	        if(find){
	            count = cur.level + 1;
	            return;
	        }
	        widthSearch(queue, end, bank, visited);
	    }
	    
	    public List<String> findNeighbors(String s, String[] bank){
	        List<String> result = new ArrayList<>();
	        for(String gene : bank){
	            int count = 0;
	            for(int i=0; i<s.length(); i++){
	                if(s.charAt(i) != gene.charAt(i))
	                    count++;
	            }
	            if(count == 1)
	                result.add(gene);
	        }
	        return result;
	    }
	    
	    class NodeInfo{
	        String s;
	        int level;
	        public NodeInfo(String s, int level){
	            this.s = s;
	            this.level = level;
	        }
	    }
	}

我们需要对图模型本身的一些算法非常的熟悉，才能在遇到具体应用可以转化为图模型的时候能够很熟练的进行求解

***

**enjoy life, coding now! :D**
